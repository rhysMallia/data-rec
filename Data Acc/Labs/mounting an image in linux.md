**Mounting a RAW image (dd)**
Use Fdisk to find the start position of the filesystem partition which we want to mount ...
(you may have to change into super user first via the `sudo SU` command)

`fdisk -l data_aqc.dd`

![[Pasted image 20230831081319.png]]
You can also use the `mmls` command ...

`mmls data_aqc.dd`

****

Once we identify the starting sector `105672`, and the sector size `512`, we can begin to mount the image.

`mount data_aqc.dd /mnt/temp -o ro,noload,loop,offset=$((sector*sectorsize))`
																							`$((1052672*512))`
- ro == read only
- noload == deal with read issues with the ex3 file format (see man page)
- offset == our starting sector

We can then use `ls /mnt/temp` to verify the mount was successful

**Unmounting**
`umount /mnt/temp`
****

**Mounting a compressed image (e01)**
Since we need to decompress, we need to mount the image as raw using `ewfmount`
`mkdir /rawimage`
`ewfmount image.e01 /rawimage`
`ls -lh /rawimage`

![[Pasted image 20230831082010.png]]
We can see that the raw image contains our ewf1 image, which we can now use in the same way ...

`fdisk -l /rawimage/ewf1`
or
`mmls /rawimage/ewf1`

`mount /rawimage/ewf1 /mnt/temp -o ro,noload,loop,offset=$((1052672*512))`
`ls /mnt/temp`


