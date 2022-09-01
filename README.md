*(Please note that is a repository based upon a template (not even a fork as there's another repo which is the fork). Details of the design are described at the very end of this `README.md`. Go to https://tinytapeout.com for instructions!)*

![](../../workflows/wokwi/badge.svg)

# What is this whole thing about?

This repo is a template you can make a copy of for your own [ASIC](https://www.zerotoasiccourse.com/terminology/asic/) design using [Wokwi](https://wokwi.com/).

When you edit the Makefile to choose a different ID, the [GitHub Action](.github/workflows/wokwi.yaml) will fetch the digital netlist of your design from Wokwi.

The design gets wrapped in some extra logic that builds a 'scan chain'. This is a way to put lots of designs onto one chip and still have access to them all. You can see [all of the technical details here](https://github.com/mattvenn/scan_wrapper).

After that, the action uses the open source ASIC tool called [OpenLane](https://www.zerotoasiccourse.com/terminology/openlane/) to build the files needed to fabricate an ASIC.

# What files get made?

When the action is complete, you can [click here](https://github.com/mattvenn/wokwi-verilog-gds-test/actions) to see the latest build of your design. You need to download the zip file and take a look at the contents:

* gds_render.svg - picture of your ASIC design
* gds.html - zoomable picture of your ASIC design
* runs/wokwi/reports/final_summary_report.csv  - CSV file with lots of details about the design
* runs/wokwi/reports/synthesis/1-synthesis.stat.rpt.strategy4 - list of the [standard cells](https://www.zerotoasiccourse.com/terminology/standardcell/) used by your design
* runs/wokwi/results/final/gds/user_module.gds - the final [GDS](https://www.zerotoasiccourse.com/terminology/gds2/) file needed to make your design


# What is this specific design about?

The design implements a 300 baud UART transmitter with limited character set (0x40..0x5F) loading. Both limitations are described in a separate section below.

The 300 baud is a theoretical value as the limited clock rate as stated in the [TinyTapeout FAQ](https://docs.google.com/document/d/1HeUJ5RWxnGo36LE1jp5CoCfBO91wTzGANzlKC_vVfFI/):

>What is the top clock speed?
>Not sure yet, I would like to get around 100kHz but with the current scan chain and 500 designs it’s looking more like 750Hz. TBD. We have a built in clock divider that can further reduce this speed down to 2Hz.

I am not sure if the actual baud rate will differ.


### Input pins

The design uses all 8 input pins:

* IN0: 300 Hz input clock signal (defining the baudrate)
* IN1: bit b0 (the least significant bit) of the loaded and transmitted character (b0)
* IN2: bit b1 of the loaded and transmitted character (b1)
* IN3: bit b1 of the loaded and transmitted character (b2)
* IN4: bit b1 of the loaded and transmitted character (b3)
* IN5: bit b1 of the loaded and transmitted character (b4)
* IN6: load word into shift register from parallel input (IN1..IN5) (`1`) or cycle the existing word with start/stop bits around it (`0`)
* IN7: output enable (for gated output signals): `1` output is enabled, `0` output is disabled (permanently set to HIGH/`1`)


### Output pins

The design uses all 8 output pins...

* OUT0: UART (serial output pin, direct throughput)
* OUT1: UART (serial output pin, gated by enable signal)
* OUT2: UART (serial output pin, reverse polarity, direct throughput)
* OUT3: UART (serial output pin, reverse polarity, gated by enable signal)
* OUT4: UART (MSBit, direct throughput); *typically set to 1 or can be used to sniffing the word cycling through the shift register)*
* OUT5: UART (MSBit, reverse polarity, direct throughput); *same usage as above*
* OUT4: UART (MSBit, gated by enable signal); *typically set to 1 or can be used to sniffing the word cycling through the shift register)*
* OUT5: UART (MSBit, reverse polarity, gated by enable signal); *same usage as above*


## Limitiations of the implementation

* The low baud rate.
* The limited character set of 0x40..0x5F (i.e. capital letters `A`..`Z`, and special printable characters `@`[\]^_`) have been chose arbitrarily to allow human-readable characters. This is because the message encoding has been limited to 5 bits (only 5 data input pins plus 3 control input pins). That means that the characters' three most significant bits are fixed to `0b010`. This results in words being `0b010X'XXXX`, i.e. between `0b0100'0000` (=`0x40`) and `0b0101'1111` (=`0x5F`).


# Status/TODOs

I am a bit late to the party. I've started to think about the design on August, 31st - and submission deadline is already one day later on September, 1st.

🔲 Describe the design idea

☑️ Implement the design idea using Wokwi

🔲 Describe the implementation

☑️ Edit the [Makefile](Makefile) and change the WOKWI_PROJECT_ID to match the project. → It's here: https://wokwi.com/projects/341631511790879314

☑️ Enable GitHub Actions

☑️ Describe the signal mapping to the ASIC hardware I/O pins/ Wokwi user interface in the simulation

🔲 Share your GDS on twitter, tag it #tinytapeout and [@matthewvenn](https://twitter.com/matthewvenn)!

🔲 [Submit it to be made](https://docs.google.com/forms/d/e/1FAIpQLSc3ZF0AHKD3LoZRSmKX5byl-0AzrSK8ADeh0DtkZQX0bbr16w/viewform?usp=sf_link)

☑️ [Join the community](https://discord.gg/rPK2nSjxy8)

🔲 Improve the implementation to work around the current limitations.


