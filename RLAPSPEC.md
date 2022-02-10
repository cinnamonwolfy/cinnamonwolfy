# Remote Login Authentication Protocol 1.0 Specifications
## by Sophie Rolong-Olivo (pocketlinux32)

## Introduction

Remote Login Authentication Protocol is an authentication protocol used to
authenticate a user over the network using a text file as a database,
primarily the password database of a Unix system (however, it can be used as a
wrapper around other file types and protocols (such as SQL)). This protocol
communicates using a server/client paradigm: The client sends login credentials
that are yet to be authenticated, and the server authenticates whatever
credentials it receives.

## Packet Layout

A valid RLAP packet always start with `RLAP` followed by the role of the system
(`SERVER` or `CLIENT`) and the version number of the protocol (`1.0` at this
time). This would be the header of the packet.

After the header, the packet would contain any of the following: a protocol
command or a data stream.

### Protocol commands

Protocol commands are commands that are used in RLAP to control the start and
end of a connection or a data stream.

#### List of protocol commands

```
RLAP_STARTCONN
RLAP_ENDCONN
RLAP_STARTLIST
RLAP_ENDLIST
```

### Data streams

A data stream is a block of data sent by either the server or the client. Its
contents depend on which system sent it (server or client). A client would send
a data stream containing login credentials to the server, and the server would
send a data stream containing authentication results back to the client.

#### Example data stream

Client
```
RLAP_STARTLIST
USER nano PLAINPASS system
USER pocket HASHPASS bupDvZGBBMoBY
... (more entries)
RLAP_ENDLIST
```

Server
```
RLAP_STARTLIST
ENTRY 1 USER YES PASS NO
ENTRY 2 USER NO
ENTRY 3 USER YES PASS YES
... (more entries)
RLAP_ENDLIST
```

## Example packets

Client
```
RLAP CLIENT 1.0
RLAP_STARTCONN
RLAP_STARTLIST
USER pocketlinux32 PLAINPASS password
RLAP_ENDLIST
```

Server
```
RLAP SERVER 1.0
RLAP_STARTCONN
RLAP_STARTLIST
ENTRY 1 USER YES PASS YES
RLAP_ENDLIST
RLAP_ENDCONN
```
