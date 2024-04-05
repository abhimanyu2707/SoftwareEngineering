---
description: It was firs created by Sun Microsystem
---

# VFS(virtual file system)

### Linux File System

* struct inode:
  * It's a physical file.
  * Contains info like inode number, owner/group, permission, timestamp
* struct dentry:
  * Contains file name.
  * Pointer to parent and children.
  * Pointer to inode
* struct file
  * Contains open mode, offset, etc.
* F->D->I&#x20;
* One inode can have multiple names(a hard link).
* process in Linux is stored using a **struct task,** which contains a list of opened files.
* ref count is used for deleting an object.
