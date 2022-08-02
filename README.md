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
