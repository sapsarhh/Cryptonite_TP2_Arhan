Step 1:
On this day, learnt about AWS which is amazon cloud services and what are the commands which are used to monitor behaviour of systems in a cloud.
Got to know about JQ which is basically like the sed and awk commands which is used to filter out data for investigational purposes.
JQ is used to filter out JSON data.
~~~
jq '.[]' book_list.json
{
  "book_title": "Wares Wally",
  "genre": "children",
  "page_count": 20
}
{
  "book_title": "Charlottes Web Crawler",
  "genre": "young_ware",
  "page_count": 120
}
{
  "book_title": "Charlie and the 8 Bit Factory",
  "genre": "young_ware",
  "page_count": 108
}
{
  "book_title": "The Princess and the Pcap",
  "genre": "children",
  "page_count": 48
}
{
  "book_title": "The Lion, the Glitch and the Wardrobe",
  "genre": "young_ware",
  "page_count": 218
}
~~~
A command like this can be used to filter out data from a document named book_list and list out various columns, also different arguments can be used with this with this command to further filter out data and get more information or rather only the info which is needed.

Step 2:
Now in this challenge, a log named rds.log had to be checked out what has been done.
for this the aforesaid command with additional arguments had to be used to check out the log and figure out who the attacker is, what ip address are they using etc.

![image](https://github.com/user-attachments/assets/a2a6e455-37e1-464c-a695-51863d9ba0ae)

![image](https://github.com/user-attachments/assets/a379fd3f-66c2-4eb3-b9b5-6b15ad6c1390)

For the first two questions, this command had to be used:
~~~
bash
jq -r '.Records[] | select(.eventSource == "s3.amazonaws.com" and .requestParameters.bucketName=="wareville-care4wares") | [.eventTime, .eventName, .userIdentity.userName // "N/A",.requestParameters.bucketName // "N/A", .requestParameters.key // "N/A", .sourceIPAddress // "N/A"]' cloudtrail_log.json
~~~

For the rest of the questions, these commands had to be used:
~~~
bash
jq -r '["Event_Time", "Event_Source", "Event_Name", "User_Name", "Source_IP"], (.Records[] | select(.sourceIPAddress=="53.94.201.69") | [.eventTime, .eventSource, .eventName, .userIdentity.userName // "N/A", .sourceIPAddress // "N/A"]) | @tsv' cloudtrail_log.json | column -t -s $'\t'
jq -r '["Event_Time","Event_Source","Event_Name", "User_Name","User_Agent","Source_IP"],(.Records[] | select(.userIdentity.userName=="PLACEHOLDER") | [.eventTime, .eventSource, .eventName, .userIdentity.userName // "N/A",.userAgent // "N/A",.sourceIPAddress // "N/A"]) | @tsv' cloudtrail_log.json | column -t -s $'\t'
grep INSERT rds.log
~~~

Learnings:
Learnt about AWS, cloudtrail,cloudwatch and how to view different logs and go through the events of a system.

