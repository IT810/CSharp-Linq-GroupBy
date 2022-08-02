# C# – LINQ GroupBy Examples
GroupBy là một chức năng LINQ cho phép nhóm các mục từ bộ sưu tập dựa trên một khóa nhất định. Nó tương đương với mệnh đề GROUP BY của SQL. Trong bài viết này, chúng tôi sẽ hiển thị các ví dụ khác nhau về việc sử dụng, bắt đầu từ nhóm đơn giản nhất theo một khóa, thông qua nhóm theo nhiều khóa, bộ chọn kết quả tùy chỉnh và tất cả những điều đó trong hai biến thể: biểu thức Lambda và truy vấn.

Hãy chuẩn bị dữ liệu mẫu mà chúng tôi sẽ thực hiện để trình bày các ví dụ khác nhau về group by. Đối với mục đích này, chúng tôi xác định lớp Person và tạo 10 đối tượng được thu thập trong danh sách.

```c#
public class Person
{
    public string Forename { get; set; }
    public string Surname { get; set; }
    public int Age { get; set; }
}
```
```c#
var people = new List<Person>()
{
    new Person() { Forename = "John", Surname = "Smith", Age = 33 },
    new Person() { Forename = "Michael", Surname = "Jones", Age = 41 },
    new Person() { Forename = "Susan", Surname = "Taylor", Age = 21 },
    new Person() { Forename = "Michael", Surname = "Evans", Age = 41 },
    new Person() { Forename = "James", Surname = "Wilson", Age = 39 },
    new Person() { Forename = "Michael", Surname = "Johnson", Age = 35 },
    new Person() { Forename = "Susan", Surname = "Davies", Age = 21 },
    new Person() { Forename = "Susan", Surname = "Robinson", Age = 47 },
    new Person() { Forename = "John", Surname = "Wright", Age = 44 },
    new Person() { Forename = "Susan", Surname = "Walker", Age = 21 }
};
```
## Single key selector
 * Kịch bản đầu tiên là bộ sưu tập người theo nhóm của Forename.
 * LAMBDA EXPRESSION
```c#
var groups = people.GroupBy(x => x.Forename);
```
 * QUERY EXPRESSION
```c#
var groups = from p in people group p by p.Forename;
```
 * Cả hai biểu thức Lambda và truy vấn đều tạo ra các kết quả giống nhau có thể được hiển thị với các vòng foreach. Chúng ta cần sử dụng hai trong số đó làm cấp độ đầu tiên là bộ sưu tập các nhóm và mỗi nhóm chứa bộ sưu tập những người trong nhóm cụ thể.
```c#
foreach (var group in groups)
{
    Console.WriteLine($"Group key: {group.Key}");
    foreach (var person in group)
    {
        Console.WriteLine($"Forename: {person.Forename}, Surname: {person.Surname}, Age: {person.Age}");
    }
    Console.WriteLine();
}
```
Trong kết quả, chúng ta có thể thấy bốn nhóm, trong đó những người trong mỗi nhóm có chung tên tuổi.
![image](https://user-images.githubusercontent.com/55732539/182334824-65043d27-886c-4d69-a5d7-583b0c6a04f1.png)

## Multiple key selector
 * Ví dụ trên là đơn giản nhất nhưng cũng có thể nhóm theo nhiều khóa. Để trình bày nó, hãy nhóm bộ sưu tập người của chúng ta theo cả forename và age.
 * LAMDA EXPRESSION
```c#
var groups = people.GroupBy(x => (x.Forename, x.Age));
```
 * QUERY EXPRESSION
```c#
var groups = from p in people group p by (p.Forename, p.Age);
```
 * Kết quả có thể được in bằng mã từ ví dụ trước. Lần này chúng tôi có bảy nhóm người, nơi mỗi nhóm chỉ chứa những người có cùng forename và age.
 ![image](https://user-images.githubusercontent.com/55732539/182339472-68448a78-4930-4c48-b207-7b784d896c1d.png)
 
## Custom result selector
 * Ví dụ cuối cùng tôi muốn trình bày ở đây là kết hợp nhóm bằng cách chọn kết quả tùy chỉnh. Trong kịch bản này, mỗi nhóm trong bộ sưu tập được trả về có thuộc tính GroupName chứa một tên khóa, GroupSize chứa số lượng mục trong một nhóm và GroupItems có chứa danh sách người trong một nhóm.
 * LAMBDA EXPRESSION
```c#
var groups = people.GroupBy(x => (x.Forename)).Select(x => new
{
    GroupName = x.Key,
    GroupSize = x.Count(),
    GroupItems = x.ToList()
});
```
 * QUERY EXPRESSION
```c#
var groups = from p in people
             group p by p.Forename
             into g
             select new
             {
                 GroupName = g.Key,
                 GroupSize = g.Count(),
                 GroupItems = g.ToList()
             };
```
 * Code để hiển thị kết quả cần được sửa đổi một chút để phản ánh các thay đổi chọn trên.
```c#
foreach (var group in groups)
{
    Console.WriteLine($"Group name: {group.GroupName}");
    Console.WriteLine($"Group size: {group.GroupSize}");
    foreach (var person in group.GroupItems)
    {
        Console.WriteLine($"Forename: {person.Forename}, Surname: {person.Surname}, Age: {person.Age}");
    }
    Console.WriteLine();
}
```
![image](https://user-images.githubusercontent.com/55732539/182340980-ba030fd1-250a-4116-8446-18d034eb504f.png)
