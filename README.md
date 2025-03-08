# Hackintosh EFI for HP Envy 13-ad1xx  
**Updated for 2025 – Supports macOS Ventura, Sonoma, and Sequoia**

This EFI is an enhanced version of the OpenCore MOD EFI originally developed by [Olarila](https://olarila.com/). I’ve customized it to optimize compatibility and functionality for the HP Envy 13-ad1xx, ensuring it works seamlessly with the latest macOS releases as of March 2025. Key improvements include the addition of `SSDT-XOSI.aml`, an updated `VoodooPS2.kext` for trackpad fixes, resolved Bluetooth issues for Broadcom cards, and added Wi-Fi functionality. This EFI is tailored for stability and performance on Ventura (13.x), Sonoma (14.x), and Sequoia (15.x).

## Key Enhancements
- **SSDT-XOSI.aml**: Integrated to improve ACPI compatibility by redirecting OSI calls, ensuring better power management and hardware recognition across macOS versions.
- **Updated VoodooPS2.kext**: Upgraded to the latest version (debug build recommended for Sequoia) to fix trackpad issues, providing smoother and more reliable input on the HP Envy 13-ad1xx.
- **Broadcom Bluetooth Fix**: Addressed Bluetooth connectivity for Broadcom cards (e.g., BCM94352HMB) by adjusting kexts like `BrcmPatchRAM3.kext` and `BrcmBluetoothInjector.kext`, ensuring full functionality.
- **Wi-Fi Support**: Added support for Wi-Fi using compatible Broadcom or Intel cards (e.g., with `AirportBrcmFixup.kext` or `itlwm.kext`), depending on your hardware configuration.

## Installation and Configuration
To use this EFI effectively, follow these steps:

1. **Download the EFI**: Obtain the latest version from the provided source (e.g., a GitHub repository or Olarila’s site) and copy it to your EFI partition.
2. **Customize SMBIOS**: Inject your unique SMBIOS data into the `config.plist` file to ensure proper macOS recognition and avoid hardware ID conflicts. Use [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) to generate a unique SMBIOS (e.g., MacBookPro14,1 or iMac18,1) with a valid serial number, MLB, and UUID. Refer to the [Dortania OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/extras/smbios-support.html#miscellaneous-smbios) for detailed instructions.
   - Open `config.plist` with a tool like [ProperTree](https://github.com/corpnewt/ProperTree) or OpenCore Configurator.
   - Update the `PlatformInfo` section with your generated values (e.g., `SystemSerialNumber`, `MLB`, `SystemUUID`).
   - Set `ROM` to your network card’s MAC address (remove colons) for network consistency.
3. **Hardware Compatibility**: Verify your Wi-Fi/Bluetooth card (e.g., Broadcom BCM94360NG or Intel AX200 with `itlwm`) matches the kexts included. For Broadcom, ensure `AirportBrcmFixup.kext` and related patches are active. For Intel, use `itlwm.kext` and `IntelBluetoothFirmware.kext`.
4. **BIOS Settings**: Update to the latest HP Envy 13-ad1xx BIOS (e.g., F.18 or later) and disable CFG-Lock, VT-d, and Secure Boot if possible to avoid boot issues.
5. **Testing**: Boot with verbose mode (`-v` boot arg) to troubleshoot. Adjust `boot-args` (e.g., `-lilubetaall`, `amfi_get_out_of_my_way=1`) in `config.plist` if needed for Sequoia compatibility.

## Notes and Considerations
- **Stability**: Tested on Ventura, Sonoma, and Sequoia betas as of March 2025. Sequoia may require additional tweaks (e.g., disabling legacy Broadcom support) due to Apple’s evolving hardware requirements.
- **Limitations**: Audio (e.g., Realtek ALC283) and external display (via Type-C) may need further patching (e.g., `SSDT-HPET` or `WhateverGreen` adjustments). Check Olarila forums or Dortania guides for updates.
- **Safety**: Use a separate drive or USB installer for initial testing to avoid disrupting existing macOS installs. Disable SIP partially (e.g., `csr-active-config=0x67`) if kext loading fails.
- **Community Feedback**: Share your experience on hackintosh forums or X to help refine this EFI for others with the HP Envy 13-ad1xx.

## Credits
This build builds upon Olarila’s OpenCore MOD EFI foundation. Special thanks to the hackintosh community, including Dortania’s guides and CorpNewt’s tools, for enabling these customizations.


