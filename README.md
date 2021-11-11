# addmember-telegram
Sử dụng `python 3` để thêm thành viên từ Nhóm A sang Nhóm B (di chuyển thành viên trong nhóm của bạn)


## Yêu cầu
* Môi trường của python 3 (Linux, Window)
* Cần khoảng 20 tài khoản để chạy (Tránh chặn tài khoản Telegram)
* Mỗi tài khoản cần có trong Nhóm nguồn và Nhóm mục tiêu
* Thông báo cho bạn điện thoại khu vực
* Nhóm của bạn là nhóm Supper


![Supper group](images/note_tele.png)
![Upgraded Supper group](images/note_tele2.png)

## Hướng dẫn

* Bước 1: Cài đặt gói `telethon`
```
pip install telethon
```

* Bước 2: Tạo tệp config.json
Sao chép tệp config.json từ config.example.json

```
{
	"group_target": 1398120166, --> nhóm mục tiêu id
	"group_source": 1490302444, --> nhóm nguồn id
	"accounts": [ --> tài khoản
		{
			"phone": "+84XXXX",
			"api_id": 1234566,
			"api_hash": "57c6f3c72c2f21676d53be2eXXXXXX"
		}
	]
}
```
`group_target` và `group_source`: sau khi chạy get_data.py và kiểm tra tệp trong data/group
`accounts`: liệt kê tài khoản Telegram; mỗi điện thoại, tạo ứng dụng trong https://my.telegram.org/apps và có api_id, api_hash

* Bước 3: Sau khi có tệp `config.json`, hãy chạy` python init_session.py`, nhập số điện thoại và mã bạn nhận được

![Init session](images/step1.png)

* Bước 4: Chạy `python get_data.py` để lấy dữ liệu của nhóm, người dùng dữ liệu và lưu tệp vào thư mục `data`

![Get data](images/step2.png)
![Data after Get](images/data_step2.png)

```
{
    "user_id": "847587728",
    "access_hash": "2393668282771176567",
    "username": "None"
}
```
Một nhóm có một danh sách người dùng (danh sách tên người dùng), nhưng mỗi tài khoản Telegram có danh sách Người dùng (khác biệt user_id, access_hash). Sử dụng `user_id` và` access_hash` để thêm thành viên, vì vậy bạn cần có được danh sách người dùng của từng tài khoản Telegram.
Lưu ý: Sử dụng tên người dùng cũng có sử dụng để thêm thành viên, nhưng một cái gì đó sử dụng không có tên người dùng

Sau khi chạy lấy dữ liệu, hãy kiểm tra lại tệp trong data/group và chỉnh sửa cấu hình tệp để thay đổi mục tiêu nhóm, nhóm_nguồn mà bạn muốn thêm.

* Step 5: run `python add_member.py` to add member from `group_source` to `group_target`
Logic: 
	* after add 1 member, sleep 2 minutes
	* each account add 35 member --> sleep 15 minutes
	* Remove account when Exception Flood
	* Break if don't have account

Note: If your account blocked, get link https://web.telegram.org/#/im?p=@SpamBot and chat /start to see time released

![Get data](images/block.png)

Done!

## Ps: 
Because some people interesting my repository create some issue, inbox Telegram. I don't have time to solve it, so I update your script to be good. I will open issue and try to resolved it. But some thing about basic language `python`, please search Internet before create issue! Thanks!
