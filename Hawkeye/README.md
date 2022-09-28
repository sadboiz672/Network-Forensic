An accountant at your organization received an email regarding an invoice with a download link. Suspicious network traffic was observed shortly after opening the email. As a SOC analyst, investigate the network trace and analyze exfiltration attempts.

# Tools:

- [Wireshark](https://www.wireshark.org/)
- [NetworMiner](google.com)
- [Apackets](https://apackets.com/)
- [MaxMind Geo IP](https://wiki.wireshark.org/HowToUseGeoIP#:~:text=MaxMind%20produces%20databases%20and%20software,information%20for%20an%20IP%20address.)
- [VirusTotal](https://www.virustotal.com/gui/)
- Detail chall: [here](https://cyberdefenders.org/blueteam-ctf-challenges/91)

# Note:

- Đây là thử thách đàu tiên liên quan tới network forensic mà mình đã tìm hiểu, tất nhiên phân tích gói tin ở mức cơ bản mình đã làm được. Nhưng biết đâu qua những thử thách này có thể học hỏi thêm một số trick hay tool hoặc command hay hơn thì sao.... Mình đã đạt gần như tuyệt đối 95% cho thủ thách lần này bỏ có 1 câu hơi ngớ ngẩn haha !!!! cùng mình đi thử nào ~~

- Cũng như bình thường thôi, với bất kỳ bài Forensic nào cũng cần biết tổng quan thông tin có thể thu thập được. Đầu tiên mình sẽ rà qua một số thông tin địa chỉ IP, kết nối TCp, UDP, Eth...

![image](https://user-images.githubusercontent.com/42565778/191885486-92be4850-de4f-4c65-b2ff-506c8741de85.png)

- hoặc các thông tin cơ bản của gói tin

![image](https://user-images.githubusercontent.com/42565778/191885520-9d0296b6-c081-4d37-9663-872ab1b708e5.png)

 - Và sau khi đã kiểm tra tổng quan về gói tin mình đã có thể trả lời nhanh một vài câu hỏi :)))

# Chall:

1. How many packets does the capture have?

- Lấy kết quả từ việc rà soát bên trên

![image](https://user-images.githubusercontent.com/42565778/191886632-fde80946-f02f-4f08-aadc-164ef5d2a60d.png)

`_submit: 4003_`

2. At what time was the first packet captured?

- Lấy kết quả từ việc rà soát bên trên

![image](https://user-images.githubusercontent.com/42565778/191886735-385d908d-8860-489f-babe-6fa9a1e16745.png)

`_submit: 2019...._`

3. What is the duration of the capture?

- Lấy kết quả từ việc rà soát bên trên

![image](https://user-images.githubusercontent.com/42565778/191886780-33633d8d-35d9-4f8d-bdf0-90bd89dee828.png)

`_submit: 01:..._`

4. What is the most active computer at the link level?

- Lấy kết quả từ việc rà soát bên trên.

![image](https://user-images.githubusercontent.com/42565778/191886908-5bc3c19f-78bb-46df-a977-7cf188830378.png)

`_submit: 00:...._`

5. Manufacturer of the NIC of the most active system at the link level?

- Câu hỏi này ban đầu mình cũng không hiểu đang muốn tìm thông tin gì, và mình loay hoay 1 hồi khá lâu để có thể đưa ra đáp án... cần tìm hiểu NIC là gì và nó là thành phần nào trong gói tin...

![image](https://user-images.githubusercontent.com/42565778/191887265-ac862fe9-a71a-4594-8762-e29075b25aa8.png)

- Vậy mình moi thông tin NIC từ đâu trong gói tin?

![image](https://user-images.githubusercontent.com/42565778/191887371-05e011d1-d383-45ca-aa9e-a66939450711.png)

- Dựa vào thông số trước địa chỉ MAC do đó mình có tìm kiếm thêm thông tin trên gg

![image](https://user-images.githubusercontent.com/42565778/191887653-e15cf85d-9825-4df2-ae0a-0bd2a038126e.png)

![image](https://user-images.githubusercontent.com/42565778/191887768-c9bd4d4e-ad95-4463-b55a-46897047afaf.png)

- Nhưng có cách làm dễ hơn thế này mà sau khi tham khảo cách mà các chuyên gia khác sẽ làm như thế nào thì mình đã biết đc trang web: [Macaddress](https://macaddress.io/). Và đây là những gì mình đã mất hàng giờ tìm kiếm thì nó chỉ mất 1s để nhận kết quả...

![image](https://user-images.githubusercontent.com/42565778/191888054-62c4c362-1abc-4160-8e92-2d8584223695.png)

`_submit: Hewll...._`

6. Where is the headquarter of the company that manufactured the NIC of the most active computer at the link level?

- Do cùng 1 wiki cho nên là mình đã nhanh chóng tìm kiếm được địa chỉ.

![image](https://user-images.githubusercontent.com/42565778/191888157-ef556d96-b2b0-4ad9-aea9-d95e62efece2.png)

`_submit: pa...._`

7. The organization works with private addressing and netmask /24. How many computers in the organization are involved in the capture?

- Thông thường IP private sẽ là lớp A hoặc B thường là những IP dải 10, cho nên chúng ta có ngay kết quả

![image](https://user-images.githubusercontent.com/42565778/191888878-38a069c0-469d-406d-b279-377efaf1d7d8.png)

_`submit: 3`_


8. What is the name of the most active computer at the network level?

- Sử dụng một vài bộ lọc mà Networkminer cung cấp và mình đã tìm được thông tin của máy tính đó

![image](https://user-images.githubusercontent.com/42565778/191889231-5b47dda6-ecff-4001-9a12-59573ed2af8e.png)

`_submit: BEIJING....._`


9. What is the IP of the organization's DNS server?

- Nếu gặp các câu hỏi dạng như này, việc sử dụng networkminer cho chúng ta khá nhiều dữ liệu... như 10.4.10.132 là địa chỉ của máy nạn nhân, 
địa chỉ 10.4.10.255 là broadcast.... và chúng ta có 10.4... là địa chỉ DNS.

![image](https://user-images.githubusercontent.com/42565778/191890267-62368e60-673f-41c9-85af-86c64084c64e.png)

`_submit: 10.4....._`

10. What domain is the victim asking about in packet 204?

- Cũng không có gì khó lắm chỉ cần follow để xem nội dung thôi 

![image](https://user-images.githubusercontent.com/42565778/191890400-c3bc3a25-ee0d-4726-b47c-19ce492d251c.png)

`_submit: proforma......._`

11. What is the IP of the domain in the previous question?

- Kết quả hiển thị ngay trong nội dung của file pcap.

![image](https://user-images.githubusercontent.com/42565778/191894434-cb937d93-2bd7-48d3-8191-da426b1cc1c7.png)

`_submit: 217......._`

12. Indicate the country to which the IP in the previous section belongs.
- Các bạn có thể sử dụng các website check ip là ra nhé.

![image](https://user-images.githubusercontent.com/42565778/191894731-baac7cce-291a-458e-83e8-65a0b4b9faf7.png)

`_submit: Fra...._`

13. What operating system does the victim's computer run?




14. What is the name of the malicious file downloaded by the accountant?




15. What is the md5 hash of the downloaded file?





16. What is the name of the malware according to Malwarebytes?




17. What software runs the webserver that hosts the malware?



18. What is the public IP of the victim's computer?



19. In which country is the email server to which the stolen information is sent?



20. What is the domain's creation date to which the information is exfiltrated?



21. Analyzing the first extraction of information. What software runs the email server to which the stolen data is sent?



22. To which email account is the stolen information sent?



23. What is the password used by the malware to send the email?



24. Which malware variant exfiltrated the data?



25. What are the bankofamerica access credentials? (username:password)



26. Every how many minutes does the collected data get exfiltrated?


