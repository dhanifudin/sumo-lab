# Sumo Lab

## Simulation using openstreetmap

- Open [OpenStreetMap Export](https://www.openstreetmap.org/export)

 ![OpenStreetMap](./images/openstreetmap.png)

- Download then save into your directory
- Open the terminal and run the following command to convert openstreetmap into netedit format

```bash
netconvert --osm-files map.osm -o map.net.xml
```

- Generate the trips using `randomTrips.py` tools, please run following command.

```bash
/usr/share/sumo/tools/randomTrips.py -n map.net.xml -r map.rou.xml -o map.trips.xml -e 600 -p 0.5
```

- From your terminal, run

```bash
netedit map.net.xml
```

- In the netedit application, please find **File**-> **Demands Elements** -> **Load Demands Elements** (Ctrl + D)

- Load your route file (e.g map.rou.xml)

- Save the demands **File** -> **Demands Elements** -> **Save Demands Elements**, then press Ctrl + T to run the simulation using sumo-gui

- Adjust delay the simulation

- Press Play button (the green button)

- Save the simulation sumocfg **File** -> **Save Configuration** (Ctrl + Shift + S)

- Generate trace file using following command

```bash
sumo -c map.sumocfg --fcd-output trace.xml
```

- Generate mobility output as tcl file format using following command

```bash
/usr/share/sumo/tools/traceExporter.py --fcd-input trace.xml --ns2mobility-output ns2mobility.tcl
```

- Put the `ns2mobility.tcl` into your home of ns3
- Copy the `sources/aodv/examples/aodv.cc` into `<ns3-home>/src/aodv/examples/aodv.cc`
- Run the ns3 simulation by using following command

```bash
./waf --run aodv --vis
```
