BOARD=tang_nano_20K_LCD
FAMILY=GW2A-18
# DEVICE=GW2AR-LV18QN88C8/I7
DEVICE=GW2A-LV18PG256C8/I7

all: TOP.fs

# Synthesis
TOP.json: TOP.v
	yosys -p "read_verilog TOP.v; read_verilog VGA_timing.v; read_verilog gowin_rpll/gowin_rpll.v; synth_gowin -top TOP -json TOP.json"

# Place and Route
TOP_pnr.json: TOP.json
	nextpnr-gowin --json TOP.json --freq 27 --write TOP_pnr.json --device ${DEVICE} --family ${FAMILY} --cst ${BOARD}.cst

# Generate Bitstream
TOP.fs: TOP_pnr.json
	gowin_pack -d ${FAMILY} -o TOP.fs TOP_pnr.json

# Program Board
load: TOP.fs
	#openFPGALoader -b ${BOARD} TOP.fs -f # Flash
	openFPGALoader -b ${BOARD} TOP.fs # SRAM

.PHONY: load
.INTERMEDIATE: TOP_pnr.json TOP.json
