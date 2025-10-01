AreaOfWork
Id, Name
1, "Tank Blending & Metering"
2, "Gas Jetty & EWTP"

EquipmentCategory
Id, Name, AreaOfWorkId
1, "Rotating Equipment", 1
2, "Stationary Equipment", 1
3, "Instrument", 1
4, "Others", 1
5, "Rotating Equipment", 2
6, "Stationary Equipment", 2
7, "Jetty", 2
8, "Others", 2

FunctionalLocation
Id, Name, EquipmentCategory
"42-P-101AB", 1
"42-P-101CD", 1
"42-P-102AB", 1
"42-P-103AB", 1
"42-P-104AB", 1
"42-P-105AB", 1
"42-P-106AB", 1
"42-P-107AB", 1
"42-P-201AB", 1
"42-P-202AB", 1
"42-P-203ABC", 1
"42-P-204ABC", 1
"42-P-205ABC", 1
"42-P-206AB", 1
"42-P-207AB", 1
"42-P-301ABC", 1
"42-P-302AB", 1
"42-P-303AB", 1
"42-P-304AB", 1
"42-P-305", 1
"42-P-306AB", 1
"42-P-501ABC", 1
"42-P-502AB", 1
"42-P-503CDE", 1
"42-T-101A", 2
"42-T-101B", 2
"42-T-101C", 2
"42-T-101D", 2
"42-T-101E", 2
"42-T-101F", 2
"42-T-101G", 2
"42-T-102A", 2
"42-T-102B", 2
"42-T-103A", 2
"42-T-103B", 2
"42-T-104A", 2
"42-T-104B", 2
"42-T-105A", 2
"42-T-105B", 2
"42-T-106", 2
"42-T-107A", 2
"42-T-107B", 2
"42-T-107C", 2
"42-T-107D", 2
"42-T-201A", 2
"42-T-201B", 2
"42-T-202A", 2
"42-T-202B", 2
"42-T-203A", 2
"42-T-203B", 2
"42-T-204", 2
"42-T-205A", 2
"42-T-205B", 2
"42-T-206", 2
"42-T-301A", 2
"42-T-301B", 2
"42-T-301C", 2
"42-T-301D", 2
"42-T-302A", 2
"42-T-302B", 2
"42-T-303A", 2
"42-T-303B", 2
"42-T-304A", 2
"42-T-304B", 2
"42-T-304C", 2
"42-T-305A", 2
"42-T-305B", 2
"42-T-501A", 2
"42-T-501B", 2
"42-T-502A", 2
"42-T-502B", 2
"42-T-503", 2
"42-T-504", 2
"42-T-505A", 2
"42-T-505B", 2
"42-P-503AB", 5
"42-P-401AB", 5
"42-P-402ABC", 5
"42-P-403ABCD", 5
"42-P-404ABCDEF", 5
"63-P-101ABCD", 5
"63-P-102ABCD", 5
"63-P-103AB", 5
"63-P-110AB", 5
"63-P-111AB", 5
"63-P-201ABC", 5
"63-P-202ABC", 5
"63-P-203AB", 5
"63-P-301AB", 5
"63-P-302AB", 5
"63-P-303AB", 5
"63-P-306AB", 5
"63-P-307AB", 5
"63-P-308AB", 5
"63-P-309AB", 5
"63-P-401AB", 5
"63-P-402AB", 5
"63-P-403AB", 5
"63-P-501", 5
"63-P-901AB", 5
"63-T-110", 6
"42-T-401A", 6
"42-T-401B", 6
"42-T-402A", 6
"42-T-402B", 6
"42-T-403A", 6
"42-T-403B", 6
"42-T-403C", 6
"42-T-403D", 6
"42-T-404A", 6
"42-T-404B", 6
"42-T-404C", 6
"42-T-404D", 6
"42-T-404E", 6
"42-T-404F", 6
"42-T-404G", 6
"42-T-404H", 6
"63-Z-403", 6
"63-Z-304", 6
"63-Z-305AB", 6
"63-Z-311", 6
"63-Z-401", 6
"63-Z-315", 6
"63-Z-306", 6
"63-Z-201", 6
"63-Z-202AB", 6
"63-Z-203", 6
"63-Z-301", 6
"63-Z-302", 6
"63-Z-303", 6
"63-Z-312", 6
"63-Z-402", 6
"63-Z-501", 6
"Jetty", 7

ReportCategory
Id, Name
1, "Tank Daily Check"
2, "Support/Helper"
3, "Green Housekeeping"

TankType
Id, Name
1, "Floating Roof"
2, "Fixed Roof"
3, "Spherical"

Service
Id, Name
1, "M4-MIXED-1 CRUDE"
2, "AV-AVTUR"
3, "HG-GAS OIL-INTERMEDIA"
4, "R5-LONG RESIDUE"
5, "DA-DMAR"
6, "HT-NAPHTA-INTERMEDIA"
7, "HH-HOMC 97"
8, "AR/HDM NAPHTA"
9, "XT-PERTAMAX TURBO"
10, "AD-ADO/SOLAR-48"
11, "HD-HOMC 92"
12, "DZ-DECANT COMPONENT"
13, "EA-PERTALITE"
14, "DQ-PERTAMINA DEX 50 PPM, BULK"
15, "DO-DECANT OIL"
16, "FL-FLUSHING OIL"
17, "HS-SLOP"
18, "PP-PROPANE"
19, "BN-BUTANE"
20, "PG-LPG MIXED, BULK"

TankComponentGroup
Id, Name, Remarks, TankTypeId
1, "Main Tank", "", 1
2, "Tank Accessories", "", 1
3, "Tank Metering", "", 1
4, "Main Tank", "", 2
5, "Tank Accessories", "", 2
6, "Tank Metering", "", 2
7, "Main Tank", "", 3
8, "Tank Accessories", "", 3
9, "Tank Metering", "", 3

TankComponent
Id, Name, Status, Reading, Unit, TankComponentGroupId
1, "Visual Plate", "Normal", null, null, 1
2, "Manhole", "Normal", null, null, 1
3, "Drain Tank", "Normal", null, null, 1
4, "Drain Control", "Normal", null, null, 1
5, "Inlet Pipe", "Normal", null, null, 1
6, "Outlet Pipe", "Normal", null, null, 1
7, "Manual Valve at Inlet", "Normal", null, null, 1
8, "Manual Valve at Outlet", "Normal", null, null, 1
9, "Motorized Valve at Inlet", "Normal", null, null, 1
10, "Motorized Valve at Outlet", "Normal", null, null, 1
11, "Expansion Joint", "Normal", null, null, 1
12, "Lowerpoint", "Normal", null, null, 1
13, "Grounding", "Normal", null, null, 1
14, "Bounding", "Normal", null, null, 1
15, "Tank Stair", "Normal", null, null, 1
16, "Sampling Hole", "Normal", null, null, 1
17, "Roof Deck", "Normal", null, null, 1
18, "Seal Roof", "Normal", null, null, 1
19, "Drain Roof", "Normal", null, null, 1
20, "Roof Stair", "Normal", null, null, 1
21, "Pressure Safety Valve", "Normal", null, null, 1
22, "Breather Valve", "Normal", null, null, 1
23, "Mixer", "Normal", null, null, 2
24, "Lighting", "Normal", null, null, 2
25, "Blanket Gas", "Normal", null, null, 2
26, "Steam Heater", "Normal", null, null, 2
27, "Condensate", "Normal", null, null, 2
28, "Lightning Protection System", "Normal", null, null, 2
29, "Bundwall", "Normal", null, null, 2
30, "Bundwall Pit", "Normal", null, null, 2
31, "Tank Pit", "Normal", null, null, 2
32, "Temperature Gauge", "Normal", 40, "°C", 3
33, "Level", "Normal", null, "mm", 3
34, "ATG", "NA", 42.4, "°C", 3
35, "ATG", "NA", 12693, "mm", 3 
36, "Visual Plate", "Normal", null, null, 4
37, "Manhole", "Normal", null, null, 4
38, "Drain Tank", "Normal", null, null, 4
39, "Drain Control", "Normal",  null, null, 4
40, "Inlet Pipe", "Normal",  null, null, 4
41, "Outlet Pipe", "Normal",  null, null, 4
42, "Manual Valve at Inlet", "Normal",  null, null, 4
43, "Manual Valve at Outlet", "Normal",  null, null, 4
44, "Motorized Valve at Inlet", "Normal",  null, null, 4
45, "Motorized Valve at Outlet", "Normal",  null, null, 4
46, "Expansion Joint", "Normal",  null, null, 4
47, "Lowerpoint", "Normal",  null, null, 4
48, "Grounding", "Normal",  null, null, 4
49, "Bounding", "Normal",  null, null, 4
50, "Tank Stair", "Normal",  null, null, 4
51, "Sampling Hole", "Normal",  null, null, 4
52, "Roof", "Normal",  null, null, 4
53, "Pressure Safety Valve", "Normal",  null, null, 4
54, "Breather Valve", "Normal",  null, null, 4
55, "Mixer", "Normal",  null, null, 5
56, "Lighting", "Normal",  null, null, 5
57, "Blanket Gas", "Normal",  null, null, 5
58, "Steam Heater", "Normal",  null, null, 5
59, "Condensate", "Normal",  null, null, 5
60, "Lightning Protection System", "Normal",  null, null, 5
61, "Bundwall", "Normal",  null, null, 5
62, "Bundwall Pit", "Normal",  null, null, 5
63, "Tank Pit", "Normal",  null, null, 5
64, "Temperature Gauge", "Normal", 52, "°C", 6
65, "Level", "Normal", 2345, "mm", 6
66, "ATG", "NA", null, "°C", 6
67, "ATG", "NA", null, "mm", 6

TankComponentReading
Id, Value, Unit, TankComponentId