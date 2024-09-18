# How to concatenate values in a column of Flutter DataTable (SfDataGrid)?.

In this article, we will show you how to concatenate values in a column of [Flutter DataTable](https://www.syncfusion.com/flutter-widgets/flutter-datagrid).

Initialize the [SfDataGrid](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/SfDataGrid-class.html) widget with all the required properties. To achieve this, build DataGrid rows in the [DataSource](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/DataGridSource-class.html) by concatenating two or more values. Use a [Map](https://api.flutter.dev/flutter/dart-core/Map-class.html) collection as the type in the [DataGridCell](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/DataGridCell-class.html) to hold the concatenated values. This allows us to store and access different types of data together in a cell.

```dart
class EmployeeDataSource extends DataGridSource {
  EmployeeDataSource({required List<Employee> employeeData}) {
    _employeeData = employeeData
        .map<DataGridRow>((e) => DataGridRow(cells: [
              DataGridCell<Map<String, dynamic>>(
                  columnName: 'image_name',
                  value: {'image': e.image, 'name': e.name}),
              DataGridCell<int>(columnName: 'id', value: e.id),
              DataGridCell<String>(
                  columnName: 'designation', value: e.designation),
              DataGridCell<int>(columnName: 'salary', value: e.salary),
            ]))
        .toList();
  }

  List<DataGridRow> _employeeData = [];

  @override
  List<DataGridRow> get rows => _employeeData;

  @override
  DataGridRowAdapter buildRow(DataGridRow row) {
    return DataGridRowAdapter(
      cells: row.getCells().map<Widget>((e) {
        if (e.columnName == 'image_name') {
          // Handle concatenated image and name.
          final Map<String, dynamic> imageNameData =
              e.value as Map<String, dynamic>;
          return Row(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              imageNameData['image'] as Image,
              const SizedBox(width: 8.0),
              Text(imageNameData['name'].toString()),
            ],
          );
        } else {
          // Handle other cells.
          return Container(
            alignment: Alignment.center,
            padding: const EdgeInsets.all(8.0),
            child: Text(e.value.toString()),
          );
        }
      }).toList(),
    );
  }
}
```

You can download the example from [GitHub](https://github.com/SyncfusionExamples/How-to-concatenate-values-in-a-column-of-Flutter-DataTable).