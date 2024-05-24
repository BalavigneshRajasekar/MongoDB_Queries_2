# MongoDB_Queries_2
#### Find all the topics and tasks which are thought in the month of October
db.tasks.aggregate({$lookup:{from:"topics",localField:"id",foreignField:"id",as:"topic"}},{$unwind:{path:"$topic"}},{$match:{$and:[{date:{$gte:"2020-10-01",$lt:"2020-11-01"}},{"topic.date":{$gte:"2020-10-01",$lt:"2020-11-01"}}]}})

#### Find all the company drives which appeared between 15 oct-2020 and 31-oct-2020

db.company_drives.aggregate([{$match:{date:{$gte:"2020-10-17",$lt:"2020-11-01"}}}])

#### Find all the company drives and students who are appeared for the placement.
([{$lookup: {from: "company_drives", localField:"id", foreignField: "User_id
', as: "placements"}}, {$unwind: {path: "$placements"}}, {$group: {_id: "$name", placementAttend: {$sum:1}}}])

#### Find the number of problems solved by the user in codekata
db.users.aggregate([{$lookup: {from: "codekata", localField:"id", foreignField: "User_
id", as: "count"}}, {$uwind: {path: "$count"}}, {$group: {_id: "$name", totalProblem Solved: {$sum:1}}}])

#### Find all the mentors with who has the mentee's count more than 15

db.mentors.find({mentees: {$gt: "15"}}, {name:1, _id:0, mentees:1})

#### Find the number of users who are absent and task is not submitted  between 15 oct-2020 and 31-oct-2020

db. Attendance. aggregate([{$lookup: {from: "tasks", localField:"id", foreignField:"id", as: "task
s"}}, {$unwind: {path: "$tasks"}}, {$match: {$and: [{date: {$gte: "2020-10-15",$lt: "2020-11-01"}},{"tasks.date": {$gte: "2020-10-15", $it: "2020-
11-01"}}]}},{$match: {$and: [{status: "absent"},{"tasks.status": "not-submitted"}]}}])



