# C# – LINQ GroupBy Examples
GroupBy là một chức năng LINQ cho phép nhóm các mục từ bộ sưu tập dựa trên một khóa nhất định. Nó tương đương với mệnh đề GROUP BY của SQL. Trong bài viết này, chúng tôi sẽ hiển thị các ví dụ khác nhau về việc sử dụng, bắt đầu từ nhóm đơn giản nhất theo một khóa, thông qua nhóm theo nhiều khóa, bộ chọn kết quả tùy chỉnh và tất cả những điều đó trong hai biến thể: biểu thức Lambda và truy vấn.

Hãy chuẩn bị dữ liệu mẫu mà chúng tôi sẽ thực hiện để trình bày các ví dụ khác nhau về group by. Đối với mục đích này, chúng tôi xác định lớp Person và tạo 10 đối tượng được thu thập trong danh sách.

'''C#
public class Person
{
    public string Forename { get; set; }
    public string Surname { get; set; }
    public int Age { get; set; }
}
'''
