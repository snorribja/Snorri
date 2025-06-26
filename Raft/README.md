## Overview

This project implements a distributed consensus system using the Raft algorithm. It uses UDP for communication and Protocol Buffers for message formatting. The system consists of multiple server nodes and one or more clients. Each server maintains a replicated log and participates in leader election and log replication to ensure fault-tolerant consensus. The client sends string commands to a server, which are then replicated across the cluster.

## File Structure

The project includes the following files:

- `raftserver.go`: Implements Raft server behavior, including state transitions, message handling, leader election, and log replication.
- `raftclient.go`: A simple command-line client that sends commands to a Raft server over UDP.
- `servers.txt`: A text file listing all server addresses (host:port), one per line.
- `Distributed Consensus - Questions.pdf`: A detailed explanation and justification of how the Raft protocol was implemented.
- `README.md`: This documentation file.

## Running the System

To run a server, use the following command:

```bash
go run raftserver.go server-host:server-port servers.txt
```

Each server must be listed in `servers.txt`, one per line:
localhost:2000
localhost:2001
localhost:2002

To run the client:

```bash
go run raftclient.go server-host:server-port
```

Then enter any valid command such as `insert`, `update`, or any string composed of letters, digits, underscores, or dashes. Type `exit` to quit the client.

## Server Behavior

Servers operate in one of four states: Follower, Candidate, Leader, or Failed. They use randomized timeouts to initiate elections, vote for candidates, and replicate logs through AppendEntries messages. Only the leader accepts and logs new client commands. These commands are committed once replicated to a majority of servers and then written to a local file named after the server (e.g., `localhost-2000.log`).

At runtime, servers accept the following console commands:

- `log`: Print committed log entries.
- `print`: Display the server's current term, role, voted leader, commit index, and more.
- `suspend`: Enter the Failed state, simulating a crash (the server will still receive but not respond to messages).
- `resume`: Exit the Failed state and return to Follower.

## Client Behavior

The client is an interactive terminal application that reads user input, validates it, and sends it to a specified server using UDP. It does not wait for server responses or acknowledgments. The command must match the regular expression `[a-zA-Z0-9_-]+`. If the command is invalid, the client prints a message and skips sending. The client cannot deadlock, even if the server is unresponsive, because it uses non-blocking communication and does not rely on responses.

## Raft Protocol Implementation

This implementation follows Raft’s specifications, especially the core parts described in Section 5 and Figure 2 of Ongaro and Ousterhout’s paper. Key aspects include:

- Leader election with majority voting and randomized election timeouts.
- Log replication using AppendEntries RPCs, ensuring log consistency.
- Commitment only when a majority of servers replicate an entry from the current term.
- Commands are applied in order, exactly once, and safely written to disk.
- Servers use mutexes and goroutines to manage concurrent access and prevent deadlocks.

All messages are defined using the pre-specified protobuf message format and sent over UDP. No RPC, TCP, or middleware is used.

## Message Format

All messages are based on the `Raft` message structure defined at [github.com/mkyas/miniraft](https://github.com/mkyas/miniraft). This includes vote requests/responses, append entries, and command submissions.

## Logging and Verification

Each server writes committed commands to a local log file named `server-host-port.log`. Entries follow the format: term,index,command

Logs across all servers should match in order and content, confirming consistency.

## Documentation

All protocol mapping, concurrency strategy, deadlock avoidance, heartbeat mechanism, and safety justification are provided in the file `Distributed Consensus - Questions.pdf`.

## Notes

This project does not include log compaction or dynamic configuration changes. Client acknowledgments are not implemented, as allowed by the assignment. No persistent state is stored across reboots; suspend and resume simulate crashes and recovery.

## References

Ongaro, D., & Ousterhout, J. (2014). _In Search of an Understandable Consensus Algorithm_. https://raft.github.io/raft.pdf  
Steen, M. van, & Tanenbaum, A. S. (2023). _Distributed Systems (4.01)_. https://www.distributed-systems.net/
