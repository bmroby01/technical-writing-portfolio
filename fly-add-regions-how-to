## How to Move Your App to a New Region

This guide will show you how to move a Fly.io app, which includes at least a single Fly Machine and an attached Fly Volume, from one region to another using `flyctl` commands.

## Prerequisites

- `flyctl` installed and configured
- Ensure you have a simple Fly.io app with one Machine and one Volume. If not, [follow these steps to install](https://fly.io/docs/hands-on/install-flyctl/) and [these steps to launch a new app with a fly volume](https://fly.io/docs/apps/volume-storage/#launch-a-new-app-with-a-fly-volume).

### 1. Determine Your Current Configuration

Check the current configuration of your app, particularly the region and volume details:

```sh
fly status
fly volumes list
```

### 2. Create a Fork of Your Volume

Create a fork, or clone, of your current Volume:

```sh
fly volumes fork <volume id> --region <region>
```
Replace  and `<volume id>` with your Volume ID which can be found with `fly volume list` and `<region>` with the [target region code](https://fly.io/docs/reference/regions/)

### 3. Create a Clone of your Machine

Create a clone of your current machine to preserve the data:

```sh
fly machine clone <machine id> --region <region code> --attach-volume <volume id>:<destination mount path>`
```

Replace `<machine id>` with the origin Machine id which can be found with `fly machine list`, `<region code>` with [target region code](https://fly.io/docs/reference/regions/), and `<volume id> with with your newly forked Volume id. 

`<destination-mount-path>` is the directory where the volume should be mounted on the file system. Note that you can’t mount a volume with a destination-mount-path of /, since / is used for the root file system.

Example Output:

```sh
Cloning Machine e286015bd6e486 into region iad
Info: --attach-volume is overriding previous mount point from `/data` to `/data`.
Attaching existing volume vol_vg7gwk7wkdqjqkzv
Provisioning a new Machine with image docker-hub-mirror.fly.io/flyio/hellofly:latest...
  Machine 32871533f12398 has been created...
  Waiting for Machine 32871533f12398 to start...
No health checks found
Machine has been successfully cloned!
```

### 4. Update the App Configuration

Update your app configuration to set the new primary region in the fly.toml file.

### 5. Remove the Old Machine and Volume

Finally, remove the old Machine and Volume to complete the migration:

```sh
fly machine remove <MACHINE_ID>
fly volume delete <VOLUME_ID>
```

Replace `<MACHINE_ID>` and `<VOLUME_ID>` with the IDs of the old Machine and old Volume, which you can find from `fly machines list` and `fly volumes list` respectively.

## Conclusion

Your Fly.io app is now successfully moved to a new region with all data preserved.