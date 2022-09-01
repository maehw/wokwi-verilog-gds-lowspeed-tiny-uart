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

...


## Input signals

...

## Output signals

...

## The Logic
...


## Limitiations of the implementation

...


### Input pins

The design uses all 8 input pins:

...


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


