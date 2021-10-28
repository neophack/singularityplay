
# ubuntu20.04 problem
```
int _singularity_image_squashfs_mount(struct image_object *image, char *mount_point) {
    char *loop_dev = NULL;

    if ( ( loop_dev = singularity_image_bind(image) ) == NULL ) {
        singularity_message(ERROR, "Could not obtain the image loop device\n");
        ABORT(255);
    }

    singularity_message(VERBOSE, "Mounting squashfs image: %s -> %s\n", loop_dev, mount_point);
    if ( singularity_mount(loop_dev, mount_point, "squashfs", MS_NOSUID|MS_RDONLY|MS_NODEV, "errors=remount-ro") < 0 ) {
        singularity_message(ERROR, "Failed to mount squashfs image in (read only): %s\n", strerror(errno));
        ABORT(255);
    }

    return(0);
}
```
delete errors=remount-ro
