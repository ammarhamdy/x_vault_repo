
**RPC (Remote Procedure Call) services** allow a program on one machine (the **client**) to request services or functions to be executed on another machine (the **server**) as if it were a local call. 

This makes it easier to build distributed systems.

---

# **What is RPC in Simple Terms?**

Imagine you're calling a friend and asking them to do something for you, like check the weather. 

You don't need to know how they get the info—you just get the result. 

That’s how RPC works in computing:
- You call a function.
- That function runs on another machine.
- You get back the result—without needing to worry about the details.

---

# **Key Concepts of RPC**

|Component|Description|
|---|---|
|**Client**|The machine or program that initiates the request.|
|**Server**|The remote machine that performs the requested task.|
|**Stub**|Code that handles the communication; acts as a "proxy" for local function.|
|**Transport**|Data is typically sent via TCP, UDP, or HTTP/S.|
|**Serialization**|Data is converted to a format that can be transmitted (like JSON, XML).|

---

# Common RPC Implementations

| RPC Type        | Technology Example   | Protocol          |
| --------------- | -------------------- | ----------------- |
| **Traditional** | SunRPC (used in NFS) | ONC/RPC           |
| **Modern**      | gRPC by Google       | HTTP/2 + Protobuf |
| **Web-based**   | JSON-RPC, XML-RPC    | HTTP              |

---

# **Where Are RPC Services Used?**

- **Linux systems:** `NFS` (Network File System) uses RPC to share directories.

- **Microservices:** `gRPC` is widely used to connect services efficiently.

- **Cloud apps:** Backend systems calling internal services over the network.

- **Windows OS:** Uses RPC for networked services and remote management.