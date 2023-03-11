# Process Containerization on LINUX

Isolate a process on Linux means using a concept called Namespaces (NS).

A namespace (NS) “wraps” some global system resource to provide resource isolation.

## Linux supports following Namespaces types
- Mount (CLONE_NEWNS; 2.4.19, 2002)
- UTS (CLONE_NEWUTS; 2.6.19, 2006)
- IPC (CLONE_NEWIPC; 2.6.19, 2006)
- PID (CLONE_NEWPID; 2.6.24, 2008)
- Network (CLONE_NEWNET; 2.6.29, 2009)
- User (CLONE_NEWUSER; 3.8, 2013)
- Cgroup (CLONE_NEWCGROUP; 4.6, 2016)
- Time (CLONE_NEWTIME; 5.6, 2020)

``` mermaid
flowchart TD
    init ==> process-a
    init ==> bash:::staged
    process-a ==> process-b

    init -.- mnt
    init -.- uts
    init -.- nw
    init -.- usr
    init -.- time
    init -.- pid
    init -.- ipc
    init -.- cgp
    process-a -.- mnt
    process-a -.- uts
    process-a -.- nw
    process-a -.- usr
    process-a -.- time
    process-a -.- pid
    process-a -.- ipc
    process-a -.- cgp
    process-b -.- mnt
    process-b -.- uts
    process-b -.- nw
    process-b -.- usr
    process-b -.- time
    process-b -.- pid
    process-b -.- ipc
    process-b -.- cgp
    bash -.- mnt
    bash -.- uts
    bash -.- nw
    bash -.- usr
    bash -.- time
    bash -.- pid
    bash -.- ipc
    bash -.- cgp
    subgraph ns::mnt
        mnt[1]
    end
    subgraph ns::uts
        uts[1]
    end
    subgraph ns::nw
        nw[1]
    end
    subgraph ns::usr
        usr[1]
    end
    subgraph ns::time
        time[1]
    end
    subgraph ns::pid
        pid[1]
    end
    subgraph ns::ipc
        ipc[1]
    end
    subgraph ns::cgp
        cgp[1]
    end
    classDef staged stroke:#f96,stroke-width:4px;
```
