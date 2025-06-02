# aggregationAssignmentMedium

### Medium Difficulty

**1. Total Quantity of Products by Supplier:**

<pre>

db.products.aggregate ([
    {
        $group: {
            _id: "$supplier.name",
            quantity: {$sum: "$quantity"}
        }
    },
  	{
				$sort: {quantity: -1}
		}
])
 
</pre>

![image](https://github.com/user-attachments/assets/5f3f9da6-841d-44b4-8e3d-714af63162e3)


**2. Average Price of Products per Tag:**

<pre>
 
db.products.aggregate([
    {
        $unwind: "$tags"
    },
    {
        $group: {
            _id: "$tags",
            avg_price: {$avg: "$price"}
        }
    },
  	{
				$sort: {avg_price: -1}
		}
])

</pre>
 
![image](https://github.com/user-attachments/assets/23d081ae-e82c-4661-8478-1f0992d60807)  
![image](https://github.com/user-attachments/assets/ab3f4a8c-81d5-49ad-9653-c901afe94dd7)  
![image](https://github.com/user-attachments/assets/3879a98d-9e41-44bc-821b-cf6a9ee283ab)



**3. Products Added in February 2023:**

<pre>
db.products.aggregate([
    {
        $match: {
            date_added: {
                $gte: new ISODate("2023-02-01T00:00:00Z"),
                $lt: new ISODate("2023-03-01T00:00:00Z")
            }
        }
    },
    {
        $project: {
            _id: 0,
            name: 1,
            category: 1,
            date_added: {
                $dateToString: {
                    format: "%Y-%m-%d",
                    date: "$date_added"
                }
            }
        }
    }
])
 
</pre>

![image](https://github.com/user-attachments/assets/f6a12893-d961-45c1-a5a8-0c2445006a9b)
