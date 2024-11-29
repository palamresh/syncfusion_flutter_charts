# syncfusion_flutter_charts

import 'package:flutter/material.dart';
import 'package:syncfusion_flutter_charts/charts.dart';

class HomeScreen extends StatefulWidget {
  const HomeScreen({super.key});

  @override
  State<HomeScreen> createState() => _HomeScreenState();
}

class _HomeScreenState extends State<HomeScreen> {
  List chartData = [
    [40, "Rent", Color.fromRGBO(82, 90, 255, 1)],
    [12, "Groceries", Color.fromRGBO(46, 198, 255, 1)],
    [20, "Utilities", Color.fromRGBO(123, 201, 82, 1)],
    [25, "Entertainment", Color.fromRGBO(3, 3, 255, 1)],
    [15, "Transportation", Color.fromRGBO(46, 3, 3, 1)],
    [10, "Others", Color.fromRGBO(416, 30, 3, 1)],
  ];

  List foodData = [
    ["Tea", 120, 80],
    ["Fish", 150, 100],
    ["Grains", 180, 150],
    ["Fuel", 200, 120],
  ];
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        backgroundColor: Color.fromRGBO(46, 198, 255, 1),
        title: Text("Chart"),
        actions: [IconButton(onPressed: () {}, icon: Icon(Icons.clear))],
      ),
      body: Column(
        children: [
          SfCartesianChart(
            primaryXAxis: CategoryAxis(
              title: AxisTitle(text: "Comodities Exchange"),
            ),
            primaryYAxis: CategoryAxis(
              title: AxisTitle(text: "Import / Expert in millions 2024"),
            ),
            legend: Legend(isVisible: true),
            series: [
              ColumnSeries(
                dataSource: foodData,
                xValueMapper: (data, _) => data[1],
                yValueMapper: (data, _) => data[1],
                color: Colors.orange,
                name: "Import",
                dataLabelMapper: (data, index) => data[0],
                dataLabelSettings: DataLabelSettings(isVisible: true),
              ),
              ColumnSeries(
                dataSource: foodData,
                xValueMapper: (data, _) => data[1],
                yValueMapper: (data, _) => data[2],
                color: Colors.green,
                name: "Export",
                dataLabelMapper: (data, index) => data[0],
                dataLabelSettings: DataLabelSettings(isVisible: true),
              )
            ],
          ),
          Padding(
            padding: EdgeInsets.all(20),
            child: SfCircularChart(
              margin: EdgeInsets.all(0),
              series: [
                DoughnutSeries(
                  dataSource: chartData,
                  yValueMapper: (data, _) => data[0],
                  xValueMapper: (data, _) => data[1],
                  radius: '70%',
                  // innerRadius: "40%",
                  // maximumValue: 50.0,
                  // explode: true,
                  // pointColorMapper: (data, _) => data[2],
                  dataLabelMapper: (data, index) {
                    return data[0].toString() + " K";
                  },
                  dataLabelSettings: DataLabelSettings(
                      isVisible: true,
                      labelPosition: ChartDataLabelPosition.outside
                      //   color: Colors.transparent,
                      ),
                ),
              ],
              legend: Legend(
                  isVisible: true,
                  position: LegendPosition.bottom,
                  iconHeight: 30,
                  orientation: LegendItemOrientation.vertical),
            ),
          )
        ],
      ),
    );
  }
}
