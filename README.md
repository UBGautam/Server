🔹 NFS Server:
NFS (Network File System) is a protocol developed by Sun Microsystems.
It allows a computer (the server) to share its files and directories over a network.
Other computers can access those files as if they were on their own local storage.
Typically used in Linux/Unix environments for centralized file storage.
Example: A company stores user home directories on an NFS server, so employees can log in from any workstation and still access their files.
Key points:
Runs on TCP/UDP port 2049.
Controlled by exports file (/etc/exports) on the server, where you define what folders are shared and who can access them.
Can use authentication, permissions, and mount options (read-only, read-write, etc.).

🔹 NFS Client:
A client is any system that connects to the NFS server to access the shared files.
On Linux, clients use the mount command to attach the remote NFS directory to their local filesystem.
After mounting, users can read/write files as though the data is on their machine.

✅ So in short:
NFS server → Shares files/directories over network.
NFS client → Mounts and accesses those files.

🔹 What “user ID mount” means in NFS
When a client mounts a directory from an NFS server, file permissions are based on UIDs (User IDs) and GIDs (Group IDs), not on usernames.
On Linux/Unix systems, every user has a numeric UID.
Example: root = UID 0, ub (your user) = UID 1000, etc.
When the client accesses files on the NFS share, the server sees only the UID/GID, not the actual username.
👉 This means that for proper permission handling, the UIDs and GIDs on client and server must match.

rootユーザー制限 (root user restriction) in short means:
On many systems (like NFS, SSH, or Linux in general), the root user (UID 0) is restricted from doing dangerous things to improve security.
Examples:
NFS: root on the client is mapped to nobody on the server (root_squash) → prevents remote root from having full control.
SSH: many servers disable direct root login (PermitRootLogin no) → you must log in as a normal user, then use sudo.
Linux system: some commands or files are only accessible to root, but you can’t run them if restrictions are set.
👉 In short: root user restrictions are security measures that block or limit root’s power when accessing from outside (network, NFS, SSH, etc.).

🔹 Evolution of NFS Versions
NFSv2 (RFC 1094, 1989)
Very old, now obsolete.
Used UDP only.
32-bit file size limit (only 2GB max).

NFSv3 (RFC 1813, 1995)
Still widely used.
Supports 64-bit file sizes (can handle >2GB files).
Works over TCP or UDP.
Better error reporting.
Asynchronous writes → faster performance.
Stateless protocol (server doesn’t keep track of client sessions).

NFSv4 (RFC 3530, 2003)
Big redesign.
Works only over TCP (more reliable).
Added stateful protocol (server keeps track of locks, sessions).
Built-in authentication (Kerberos, RPCSEC_GSS).
Cross-platform support (UNIX + Windows).
Firewall-friendly (uses port 2049 only).

NFSv4.1 (RFC 5661, 2010)
Adds pNFS (parallel NFS) → clients can read/write directly to multiple storage servers in parallel.
Improves scalability for large datacenters and clusters.

NFSv4.2 (RFC 7862, 2016 – latest stable)
Adds server-side copy (copy files without sending all data over the network).
Adds space reservations, sparse files, data cloning.
Enhanced security + performance.

🔹 Which version is used today?
Most modern Linux distros default to NFSv4.2.
Enterprises may still use NFSv3 for compatibility (especially with legacy systems).
NFSv2 is obsolete.










