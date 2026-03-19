dove vengono salvati tutti gli attributi del file 

```c
//PARAMETRI STRUTTURA STAT 
struct stat {
dev_t st_dev; /* ID of device containing file */
ino_t st_ino; /* i-number */
mode_t st_mode; /* protection & file type */
nlink_t st_nlink; /* number of hard links */
uid_t st_uid; /* user ID of owner */
gid_t st_gid; /* group ID of owner */
dev_t st_rdev; /* device ID (if special file) */
off_t st_size; /* total size, in bytes */
blksize_t st_blksize; /* blocksize for file system I/O */
blkcnt_t st_blocks; /* number of blocks allocated */
time_t st_atime; /* time of last access */
time_t st_mtime; /* time of last modification */
time_t st_ctime; /* time of last status change */
};
```

per interpretare il valore di _st_mode:
- S_ISREG(mode) controlla se è un file regolare
- S_ISDIR(mode) controlla se è una directory 
- S_ISCH(mode) controlla se è un dispositivo a caratteri 
- S_ISBLK(mode) controlla se è un dispositivo a blocchi 
