# international_telephone_area_code_list

中文下滑查看

The **international_telephone_area_code_list.json** file contains the original name and area code of 252 countries or regions. The content comes from the [countries.json](https://raw.githubusercontent.com/dr5hn/countries-states-cities-database/master/countries.json) file in the [countries-states-cities-database](https://github.com/dr5hn/countries-states-cities-database) .

 I only keep the English name of the country or region, the country or region code, the telephone area code of the country or region, and the original name (written in the language of that area) that I need.

The telephone area code of the country or region contains `-`, with or without it does not affect the use (for example, `+35818` and `+358-18` are both correct representations of its telephone area code and can be used interchangeably).

The `flags` contain the flags of 256 countries or regions, sourced from [flutter_country_code](https://github.com/mustafa-707/flutter_country_code), corresponding to the `area_code` in the `json` file. If used, `area_code` needs to be converted to lowercase to match the flag name. The proportions of most country and regional flags are 2:3 and 2:1. Choose between these two sizes if you need to display the flag size. If you need to extract more content from [countries.json](https://raw.githubusercontent.com/dr5hn/countries-states-cities-database/master/countries.json) , you can use the following demo code (only **Dart** code is shown here):

```dart
dart
void main(List<String> args) { 
 modifyCountriesJson('./countries.json');
}
void modifyCountriesJson(String jsonPath) {
 List<dynamic> countries = jsonDecode(File(jsonPath).readAsStringSync());
 for (int i = 0; i < countries.length; i++) {
  Map<String, dynamic> country = countries[i];
  // Required Key
  country.removeWhere((key, value) => 
   key != 'name' && 
   key != 'iso2' && 
   key != 'phone_code' &&
   key != 'native');
 }
 
 String updatedJson = jsonEncode(countries);
 File(jsonPath)..writeAsStringSync(updatedJson);
}
```

The `phone_code` obtained by the above method mostly does not start with `+`. In international standards, the telephone area codes of all countries and regions start with `+`. So when used for international calls and SMS, `+` needs to be added. You can judge whether there is `+` when using it to add it. You can also use the following method to add `+` to all results:

```dart
dart
void addPlusToPhoneCode(String countriesFile) {
 List<dynamic> countries = jsonDecode(File(countriesFile).readAsStringSync());
 for (var country in countries) {
   var phoneCode = country['phone_code'];
   if (!phoneCode.startsWith('+')) {
     country['phone_code'] = '+$phoneCode';
   }
 }

 File(countriesFile).writeAsStringSync(jsonEncode(countries)); 
}
```

Pass your `json` file to the above method. 

## 中文

**international_telephone_area_code_list.json** 文件包含了 252 个国家或地区的原始名称及电话区号，这些内容来源于仓库 [countries-states-cities-database](https://github.com/dr5hn/countries-states-cities-database) 中的 [countries.json](https://raw.githubusercontent.com/dr5hn/countries-states-cities-database/master/countries.json) 文件。我只保留了国家或地区英文名称、国家或地区区号、国家或地区电话区号、原始名称（以该地区语言书写）我需要用到的地方。

国家或地区电话区号中包含`-`，去掉和不去掉都不影响使用（比如 **+35818** 和 **+358-18** 都是其电话区号的正确表示方法,可以通用。）。

`flags` 中带有 256 个国家或地区的旗帜，来源于 [flutter_country_code](https://github.com/mustafa-707/flutter_country_code)，和`json`文件中的`area_code`对应。如果使用需要将`area_code`转为小写才能与旗帜名称相同。大部分的国家和地区旗帜比例为 2:3 和 2:1，如需显示旗帜尺寸在这两个之间选择。

如果你需要截取 [countries.json](https://raw.githubusercontent.com/dr5hn/countries-states-cities-database/master/countries.json) 文件中的更多内容，可以使用一下演示代码（这里只演示 Dart 代码）：

```dart
void main(List<String> args) {
  modifyCountriesJson('./countries.json');
}

void modifyCountriesJson(String jsonPath) {
  List<dynamic> countries = json.decode(File(jsonPath).readAsStringSync());

  for (int i = 0; i < countries.length; i++) {
    Map<String, dynamic> country = countries[i];
      // 需要保留的 key
    country.removeWhere((key, value) =>
        key != 'name' &&
        key != 'iso2' &&
        key != 'phone_code' &&
        key != 'native');
  }

  String updatedJson = json.encode(countries);
  File(jsonPath)..writeAsStringSync(updatedJson);
}
```

以上方法获得的 `phone_code` 大部分都没有以 `+` 开头。在国际标准里,所有的国家和地区的电话区号格式都是以 `+` 开头的,所以在国际电话和短信中使用时也都需要加上 `+`，你可以在使用的时候判断是否有 `+` 来加上。也可以使用以下方法为所有结果加上：

```dart
void addPlusToPhoneCode(String countriesFile) {
  List<dynamic> countries = json.decode(File(countriesFile).readAsStringSync());

  for (var country in countries) {
    var phoneCode = country['phone_code'];
    if (!phoneCode.startsWith('+')) {
      country['phone_code'] = '+$phoneCode';
    }
  }

  File(countriesFile).writeAsStringSync(jsonEncode(countries));
}
```

在以上方法传入你的 `json` 文件既可。
