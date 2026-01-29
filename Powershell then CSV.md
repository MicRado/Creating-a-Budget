## Get the CSV

<details close>
  <summary>Powershell</summary>

#### First
```
Import-Csv Transactions.csv |
Select-Object Date,Description,Debit,Balance |
Export-Csv Cut_Transactions.csv -NoTypeInformation
```

#### Then
```
Import-Csv Cut_Transactions.csv |
Select-Object Date,
@{ Name="Description"; Expression={ $_.Description -replace "\s-.*$","" } },
Debit,
Balance |
Export-Csv output_Transactions.csv -NoTypeInformation
```
- \s- → first space followed by -

- .*$ → everything after it to end of line

- Replaces it with nothing → trims cleanly

#### This ensures:
- If a dash appears later with no preceding space, it won’t accidentally match
- Stops exactly at the first " -"

</details>

<details close>
  <summary>Google Docs</summary>

---

Your sheet columns are:

A = Date  
B = Description  
C = Debit  
D = Balance

### Step 2 — Create the Summary Table

---

In an empty area of the sheet

**Click cell F1 and type:**

```Description```


**Click G1 and type:**

```Total Spent```

### Get the unique descriptions

---

**Click F2, then paste:**

```=UNIQUE(B2:B)```


You will see a list of all distinct descriptions appear automatically downward.
This is called a spilled range — you do NOT need to manually drag this one.

### Calculate total spend per description

---

**Click G2, then paste:**

```=SUMIF(B:B, F2, C:C)```


You’ll see a number appear for the first description.

### Drag the formula down

Now for the part that tripped you up:

Click cell G2 again

Look at the small blue square in the bottom-right corner of the cell

Move your mouse over it until the cursor becomes a plus (+)

Click and drag downward as far as the list in column F goes

Google Sheets will auto-copy the formula for each row.

---

<details close>
  <summary>Simple Dropdown of All Descriptions</summary>

---

### Step-by-step

- Click the cell where you want the dropdown
  - Example: J2
- In the menu:
  -Data → Data validation
- Under Criteria, choose:
  - Dropdown (from a range)

#### In the range box enter:
```F2:F```

- Click Done

---

Now cell J2 has a dropdown containing all your unique descriptions 🎉

---

## Show Total Spend for Selected Item

**Next to the dropdown, in K2, enter:**
```
=IF(J2="","", SUMIF(B:B, J2, C:C))
```

Now:

- Pick a description in J2
- K2 instantly shows total spent for that item   

</details>

---------------------------------------------------------------------------------------------    
