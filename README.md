# unixnu-nativefocaltechtouch
FT8203 touch controller support over Qualcomm GENI SPI for Samsung Galaxy Tab S7 FE Wi-Fi (SM-T733).

## SM-T733 integration

Fts8203.c implements the FT8203 controller protocol used by Samsung Galaxy
Tab S7 FE Wi-Fi (SM-T733, SM7325). The device's touch service supplies
Fts8203IO callbacks for complete SPI transactions, reset timing and progress
messages. Its transfer callback uses NativeGeniSpi on GENI SE14; the device
service owns GPIO, clocks, the vendor firmware input and XNU HID publication.

fts8203_start accepts the firmware bytes and initializes the controller.
fts8203_frame returns the complete active contact set, coordinates, and down/up
bits indexed by hardware contact ID. The caller serializes access to the
Fts8203 object's bounded wire buffers and translates frames into HID events.

## Source and license

The implementation files declare BSD-2-Clause-Patent; see LICENSE.
Protocol research used the FocalTech FT820x Android source at
https://github.com/Bush-cat/android_kernel_samsung_sm7225/tree/lineage-22.2/drivers/input/touchscreen/focaltech/ft820x
whose files retain FocalTech copyright and GPL version 2 terms. The research
download did not record a fixed revision. Those reference terms remain
applicable to reference material and are not replaced by this module's license.
Samsung firmware is a separately acquired device input and is not included.
