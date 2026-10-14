For RAM:
Program calls a malloc() function
malloc has some memory that has been taken from the Kernel and small requests are being handled from there.
If memory gets short , malloc asks kernel for more memory

What kernel is ?
Kernel is the main part of OS & whole ram is in its control

more ram from kernel is demanded through mmap ()
when that extra memory is used , returned through munmap()

Kernel does not give memory directly, it just says yes and assigns only when the memory is needed for use.

that's the reason that kernel often promises more memory then the free RAM

DATABASE EXAMPLE:
-- Database's data lives on disk and it is slow
therfore some of the data is cached in RAM

Suppose if some script is running on server and it used all the available RAM , Here comes the :
OOM (OUT OF MEMORY KILLER) :
It comes when RAM is full to shut down any running process , it shuts that process that has taken the maximum RAM

Prevention: 
We can set up a limit of RAM  for the script 
database has a setting too that reduces the probability of killing database process.
