# If the CRC does not match

During the release of **CBSD**, all profiles are checked and contain the correct amounts of CRC, however this situation may change over time - for example, OS authors released an update to the image on their resource.

In such cases, the attempt to get an image from the official site (and its mirrors) will result in a CRC amount error, while the official CBSD mirrors of the project will return the correct, but old copy.

In such cases, you need to update the checksums in the profiles and update the image.

The first thing you can do if you are in this situation - try to update your profiles with [GitHub](https://github.com/cbsd/cbsd-vmprofiles) \- then, in your situation already updated these profiles for you.

To do this, your system must have the **git** utility installed. The update occurs through the Makefile script in the _$workdir/etc_ directory. To update:

```
 make -C ~cbsd/etc profiles-update
```

You can add this operation to **crontab** for automatic periodic updates. If you do this for the first time, before you update the profile, you must initialize the git repository (it is executed only once):

```
 make -C ~cbsd/etc profiles-create
```

If there are no updates, you can help the project (and make the same users happy as you are) by creating a **GitHub** corresponding **pull-request** to change the CRC (or updating links and versions).

If you are at your own risk and want to take an ISO image, despite the discrepancy between the amounts of CRC, you have two options:

- Adjust the **sha256sum** value in a particular profile by setting **sha256sum=0**. When **sha256sum=0**, this causes **CBSD** to skip the CRC check.
Refer to the section [CBSD profiles](../jail/wf_profiles_ssi.md) for details on how to overwrite certain parameters.
- Prevent CRC checksums globally through the **BSD\_ISO\_SKIP\_CHECKSUM=\[yes\|no\]** environment variable (or configuration file), for example: env CBSD\_ISO\_SKIP\_CHECKSUM=yes cbsd bstart ..

To automatically update CRC amounts in profiles, you can use the **fetch\_iso** script, which we will discuss below.

# CBSD Mirrors project

You can create your own mirror that will store old images that are no longer on the original servers, but you still need.

Check out: https://github.com/cbsd/mirrors
