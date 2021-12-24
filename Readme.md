# initialize mongodb
# create ZenClassProgramme database
![cmd_8SVSTlbaA4](https://user-images.githubusercontent.com/91074732/147325322-f7333702-6edf-4b70-be45-44a96c8c72ed.png)

# Insert Users data
db.users.insertMany({})
![image](https://user-images.githubusercontent.com/91074732/147325717-ef6b29a8-c347-4e8e-8dc4-b65ea39a3f38.png)

# Insert Codekata data
db.codekata.insertMany({})
![image](https://user-images.githubusercontent.com/91074732/147332270-f070d390-0e9c-4b08-b5eb-4e18ce70cfdb.png)

# Insert attendance data
db.attendance.insertMany({})
![image](https://user-images.githubusercontent.com/91074732/147336932-6bb388b5-3af9-4312-a077-fa26a65a82c0.png)

# Insert topics data
db.topics.insertMany({})
![image](https://user-images.githubusercontent.com/91074732/147337757-c0acf01d-6832-4c6f-9110-17826e000559.png)

# Insert Tasks Data
db.tasks.insertMany({})
![image](https://user-images.githubusercontent.com/91074732/147338205-a0d86447-59fd-486a-a4dc-27746eb956e0.png)

# Insert Company drives data
db.company_drives({})
![image](https://user-images.githubusercontent.com/91074732/147338431-41bb2196-cd80-4f98-9a44-45af8805d0ac.png)

# Insert mentors data
db.mentors.insertMany({})
![image](https://user-images.githubusercontent.com/91074732/147338883-d6b2d0df-30e3-4f31-ab37-4ac029910024.png)

# 1.Find all the topics and tasks which are thought in the month of October
db.tasks.find({ month: { $eq: "October" } }).toArray()
db.topics.find({ month: { $eq: "October" } }).toArray()
![image](https://user-images.githubusercontent.com/91074732/147339766-ecc2413e-8d67-4c83-9317-ac1cf0712a87.png)

# 2.Find all the company drives which appeared between 15 oct-2020 and 31-oct-2020
db.company_drive.find({ date: { $gt: "10/15/2021", $lt: "10/30/2021" } });

# 3.Find all the company drives and students who are appeared for the placement.
db.attendance.aggregate([
    { $match: { "attendance": "present" } },
    {
        $lookup: {
            from: "users",
            localField: "student_id",
            foreignField: "studentd_id",
            as: "student_id"
        }
    },
    {
        $lookup: {
            from: "company_drive",
            localField: "company-1",
            foreignField: "company_id",
            as: "company-1"
        }
    },
    {
        $lookup: {
            from: "company_drive",
            localField: "company-2",
            foreignField: "company_id",
            as: "company-2"
        }
    }
]).pretty()

# 4.Find the number of problems solved by the user in codekata
db.codekata.aggregate([
    {
        $lookup: {
            from: "users",
            localField: "user_id",
            foreignField: "studentd_id",
            as: "student_info"
        }
    }
])

# 5.Find all the mentors with who has the mentee's count more than 15
db.mentors.find({Students_assign :{$gte : 15}});
