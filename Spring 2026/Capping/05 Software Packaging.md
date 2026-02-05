---
aliases:
---
● A way to assemble a collection of software  
for distribution  
	– Distribution can be physical or electronic  
● Can be ad hoc, very formal, and everything  
in between

**History**
● Software originally didn’t need to be packaged  
● The physical medium was the package  
	– Floppy diskettes for PCs  
	– Magnetic tapes for mainframes  
● Just a collection of files, with perhaps a directory or  
two  
● No need for installation, as microcomputer disks  
were self-booting  
	– Insert disk, turn on power, and start using the software

● As PC’s added hard drives, rudimentary  
installers starting appearing  
	– Mostly for file copying  
	– Limited hardware selection (i.e. CGA / EGA /  
	VGA graphics)  
	– Sound card selection

**Growing Software**
● Software sizes began to expand past 1-2 floppy disks  
	– 5¼” disks held 360KB/1.2MB  
	– 3½” disks held 720KB/1.44MB (rarely 2.88MB)  
● Disk swapping works, but only up to a point  
	– PC’s never had more than 2 floppy drives  
● Compression software began to take root  
	– PKZIP was one of the most popular ones  
		● Created deflate algorithm (RFC 1951 )  
		● Could span floppy disks!  
	– Microsoft had it’s own format (DMF) for Windows 95  
		● It shipped on 13 floppies!  
	– Other compression formats abounded (ARJ, ACE, RAR, LZH, etc.)

**Executable Installers**
● MS Windows ushered in the era of graphical  
installers  
● PCs all had hard drives, and software was  
purchased in boxes from retail stores  
● Packaging was still rudimentary  
	– Just getting data from floppy or CD-ROM to hard  
drive  
● Windows 95 required *uninstallers* for the first time  
	– Necessary for logo compatibility

**Linux Packages**
Early Linux distributions (Yggdrasil, SLS) didn’t support  
packages  
	– Just a collection of utilities and libraries with a kernel  
	● Later ones introduced packages  
		– Red Hat created .rpm (Red Hat Package Manager)  
			● Also used by SUSE  
		– Debian has .deb  
		– Slackware uses .tgz  
		– Gentoo just builds  
		everything from source!

**Packaging**
● A software package accomplishes a number of goals  
	– Contains files  
		● Executable code  
		● Libraries  
		● Documentation  
	– Notes required dependencies  
	– Contains instructions on where and how to install  
		● Scripts run during installation steps  
	– Metadata about software  
		● Version number  
		● Architecture  
		● OS

**Dependencies**
● Modern package managers try to handle  
dependencies for you  
	– Installing a package from a Linux repository will  
	automatically pull in required dependencies  
	– This works well when there is one repository with one  
	manager  
	– Package upgrades are usually seamless  
		● The hard work is done by the package maintainers  
	– However, mixing repositories can lead to  
	“dependency hell” and version problems

**Packages vs. Installers**
● Each program comes with an installer  
● Package manager is part of the OS  
● Package manager maintains a DB, but  
installer may or may not  
● Installers have huge number of vendors  
● Packages have just a few

**Making Software Consumable**
● Know your target audience  
● Each operating system has its own  
packaging requirements  
● Make sure that your design documents take  
into account how the software will be  
packaged and distributed  
● Your project will need to be installable!

**RPM**
● RedHat Package Manager  
● An archive file containing code,  
documentation, scripts, and metadata  
● Generated via rpmbuild command  
● Uses a .spec file to generate package contents  
	– Reasonably straightforward for simple  
	applications  
	– Example .spec file

● Once your build system is setup, figure out where  
your generated files live  
● Use %files section of .spec file to include them in the  
package  
● Set package description fields as necessary  
● Build RPM  
● Test it!  
	– Install / uninstall  
	– Ensure that the project runs after installation