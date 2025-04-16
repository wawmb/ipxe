# Brief introduction

iPXE 是领先的开源网络启动固件。它提供了一个完整的 PXE 实现，并通过其他功能进行了增强。

# Command

## 修改编译项

- src/config/local/general.h

```
// disable unsafe options
#undef CRYPTO_80211_WEP         /* WEP encryption (deprecated and insecure!) */
#undef CRYPTO_80211_WPA         /* WPA Personal, authenticating with passphrase */

// enable additional options
#define NET_PROTO_IPV6          /* IPv6 protocol */
#define DOWNLOAD_PROTO_HTTPS    /* Secure Hypertext Transfer Protocol */
#define DOWNLOAD_PROTO_NFS      /* Network File System Protocol */
#define IMAGE_TRUST_CMD         /* Image trust management commands */
#define NEIGHBOUR_CMD           /* Neighbour management commands */
#define NTP_CMD                 /* NTP commands */
#define CERT_CMD                /* Certificate management commands */

// 开启 console 命令以设置背景图。
#define CONSOLE_CMD             /* Console command */
#define IMAGE_SCRIPT            /* iPXE script image support */
#define IMAGE_EFI               /* EFI image support */
#define NSLOOKUP_CMD            /* DNS resolving command */
#define TIME_CMD                /* Time commands */
#define REBOOT_CMD              /* Reboot command */
#define POWEROFF_CMD            /* Power off command */
#define PING_CMD                /* Ping command */
```

- src/config/local/console.h

```
#define	CONSOLE_FRAMEBUFFER	/* Graphical framebuffer console */
```

- src/config/local/settings.h (仅支持X86)

```
#define CPUID_SETTINGS        /* CPUID settings */
```

## 编译命令

- ARM架构编译

```
make CROSS_COMPILE=aarch64-linux-gnu- ARCH=arm64 bin-arm64-efi/ipxe.efi
```

- X86架构编译

```
make bin-x86_64-efi/ipxe.efi V=s
```