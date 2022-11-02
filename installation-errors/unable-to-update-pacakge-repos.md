# Error

Downloaded debian installer for protonvpn and installed the package with apt:
`sudo apt install "$(pwd)"/protonvpn-stable-release_1.0.3_all.deb`

Ran command: `sudo apt update` 

```
Err:6 https://repo.protonvpn.com/debian stable/main all Packages
  File has unexpected size (59211 != 57172). Mirror sync in progress? [IP: 104.21.34.42 443]
  Hashes of expected file:
   - Filesize:57172 [weak]
   - SHA512:ce87b5126e491646d9a75a73a5519dd6666f5e617f1f51df4ade2d4f0abed714ee838b905bc378f07a19fc20112a263610b472688a7febdfdd3e8973080ee1ef
   - SHA256:46f0df7769b8f6b4ec8a8461535f1ec468a70138e9eadc64f8f70fec34e76a4f
   - SHA1:1a03ae8ceb03a67f7b116f559b5ea565233f2f0d [weak]
   - MD5Sum:bd4701805db37e8879e5b1d2f9e98b15 [weak]
  Release file created at: Tue, 25 Oct 2022 15:37:35 +0000
Reading package lists... Done 
E: Failed to fetch https://repo.protonvpn.com/debian/dists/stable/main/binary-all/Packages  File has unexpected size (59211 != 57172). Mirror sync in progress? [IP: 104.21.34.42 443]
   Hashes of expected file:
    - Filesize:57172 [weak]
    - SHA512:ce87b5126e491646d9a75a73a5519dd6666f5e617f1f51df4ade2d4f0abed714ee838b905bc378f07a19fc20112a263610b472688a7febdfdd3e8973080ee1ef
    - SHA256:46f0df7769b8f6b4ec8a8461535f1ec468a70138e9eadc64f8f70fec34e76a4f
    - SHA1:1a03ae8ceb03a67f7b116f559b5ea565233f2f0d [weak]
    - MD5Sum:bd4701805db37e8879e5b1d2f9e98b15 [weak]
   Release file created at: Tue, 25 Oct 2022 15:37:35 +0000

E: Some index files failed to download. They have been ignored, or old ones used instead.
```

### Theory

1. The mirror hosting the protonvpn package is currently being synchronised. Updating the package later may be a quick fix. As well as  clearing apt cache after a wait.

### Fixes attempted:

1. Changed the download source in software and update to main as per [this recommendation](https://askubuntu.com/questions/1182803/what-causes-failed-to-fetch-file-has-unexpected-size-mirror-sync-progress)
2. Added the reposiroty in /etc/apt/sources.list and ran `sudo apt update` to no avail
3. Ensured the web server was not down: `ping 104.21.34.42`

```
PING 104.21.34.42 (104.21.34.42) 56(84) bytes of data.
64 bytes from 104.21.34.42: icmp_seq=1 ttl=54 time=13.4 ms
64 bytes from 104.21.34.42: icmp_seq=2 ttl=54 time=7.16 ms
64 bytes from 104.21.34.42: icmp_seq=3 ttl=54 time=12.7 ms
64 bytes from 104.21.34.42: icmp_seq=4 ttl=54 time=5.93 ms
^C
--- 104.21.34.42 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3006ms
rtt min/avg/max/mdev = 5.933/9.812/13.440/3.305 ms
```
4. Upgraded packages and rebooted vm, to no avail
5. Cleared apt cache: `sudo apt-get clean`

### Questions asked
1. [Reddit - Unable to update upstream package repositories - protonvpn](https://www.reddit.com/r/linuxquestions/comments/yk8gov/unable_to_update_upstream_package_repositories/)
2. [Stackverflow - Unable to update upstream package repositories - protonvpn](https://stackoverflow.com/questions/74291868/unable-to-update-upstream-package-repositories-protonvpn)