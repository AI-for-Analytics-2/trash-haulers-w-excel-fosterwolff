## Missed Trash Pickups

Get the data for this assignment here: https://docs.google.com/spreadsheets/d/1O7aOHvppfeuzthEQ1pI9Y8cr5IlJOcvCzEYOLPxlM9g/edit?usp=sharing. Open the data in Excel and then load Claude for Excel.

This exercise will highlight some of the limitations for Claude in Excel.

Start by simply asking Claude to explain the spreadsheet.

1) Follow the steps below to find what % of complaints are not about missed trash pickups and then to find the top 10 non-missed pickup complaints by count.

- Ask Claude how many complaints were not about missed trash pickups?  Record this answer. 

5,198 complaints were not about missed trash pickups (out of 20,226 total).

Breakdown of the non-"Curbside/Alley Missed Pickup" rows:

Trash - Backdoor: 2,629
Trash Collection Complaint: 2,312
Damage to Property: 257
Note: "Trash - Backdoor" likely also represents missed pickups (just backdoor service rather than curbside). If you want to exclude those too, the answer would be 2,569.

- If it was not already provided, ask for a top 10 non-missed pickup complaints by count.  Do you see any issues?
Yes, there are multiple dimensions and some Requests are actually missed pick ups. 

- If you noticed any issues with Claude's output, ask about it and have it correct the errors.


- Repeat these 3 steps until you are satisfied.  It may take several iterations.


- What is the final answer?
Source sheet total: 20,226 complaints
Missed pickups by Request type ("Trash - Curbside/Alley Missed Pickup" + "Trash - Backdoor"): 17,657
Plus "Trash Collection Complaint" rows where Description contains "miss": 691
Truly non-missed-pickup complaints: 20,226 − 17,657 − 691 = 1,878

- Which types of complaints did Claude miss?
Many

- How would you ensure these errors do not slip into your workflow?
Have Claude dissect the dimensions in sequential steps.


2) Update the spreadsheet with this new information.

- Ask Claude to create a new column between Description and Address name "Missed Pickup" and set the value in this column to TRUE or FALSE.
- Get a % of missed pick ups using this new column and compare it to the value above?  Do they match?
Results — interesting:

Description contains "miss": 13,030 / 20,226 = 64.42% TRUE
Earlier count using Request type (Curbside + Backdoor): 17,657 / 20,226 = 87.30%
These do not match. The description-only method undercounts — many missed-pickup rows have descriptions that don't literally contain "miss" (e.g., they just say "didn't pick up", "skipped", "still out", etc.). Conversely, some rows flagged TRUE here might be in other Request categories where the word "miss" appears incidentally.

Want me to add a combined flag (Request type OR description contains "miss") for a more accurate signal?


3) Use the new column for further analysis.

- Which Council District has the greatest number of TRUE values? Double-check Claude by using a pivot table.
Council District 25 has the most TRUE "Missed Pickup" values at 836.

Top 5:

District	TRUE count
25	836
23	730
21	690
2	685
16	664
- Which Council District has the greatest percent of TRUE values?
Council District 31 has the highest TRUE rate at 71.33% (306 of 429 complaints).

Top 5 by % (excluding districts with <50 total complaints):

District	TRUE	Total	% TRUE
31	306	429	71.33%
34	449	634	70.82%
4	216	305	70.82%
1	477	674	70.77%
30	397	568	69.89%
District 25 (highest in raw count) ranks 11th by percentage at 67.64%.
- Did any Council Districts have 100% of their complaints due to missed trash pick ups?
No. The highest TRUE rate is District 31 at 71.33%. No council district had 100% of its complaints flagged as missed pickups (based on "miss" in the Description).
- Do the same with FALSE values.
Greatest number of FALSE: District 25 — 400 FALSE (out of 1,236 complaints).

Top 5 by FALSE count:

District	FALSE	Total
25	400	1,236
21	390	1,080
8	371	976
15	352	916
5	351	854
Greatest % FALSE: District 12 — 100% FALSE (4 of 4). Yes, one district hit 100% FALSE — but only because it has just 4 total complaints, so not statistically meaningful.

Among districts with meaningful volume, District 14 has the highest FALSE rate at 45.86% (83 of 181).
- Find which trash hauler has the greatest percent of their complaints due to missed trash pick ups?
RED RIVER has the greatest % of complaints flagged as missed pickups: 66.59% (9,586 of 14,395).

Full ranking:

Hauler	TRUE	Total	% TRUE
RED RIVER	9,586	14,395	66.59%
METRO	2,118	3,512	60.31%
WASTE IND	791	1,350	58.59%
(blank)	513	901	56.94%
Metro (lowercase)	22	68	32.35%
Note: "METRO" and "Metro" are stored as separate values due to casing. If you want them combined, let me know — combined Metro would be 2,140 / 3,580 = 59.78%.
- Which address has had the greatest number of missed trash pick ups?
5135 Hickory Hollow Pkwy — 21 missed-pickup complaints.

Top 10:

Address	Missed
5135 Hickory Hollow Pkwy	21
6007 Obrien Ave, Nashville, TN 37209	19
3710 N Natchez Ct	17
802 Crescent Rd, Nashville, TN 37205	17
12546 Old Hickory Blvd, Nashville, TN 37013	16
1816 Jo Johnston Ave, Nashville, TN 37203	14
2731 Murfreesboro Pike	13
617 Kinsey Blvd	13
110 George L Davis Blvd	12
14881 Old Hickory Blvd, Nashville, TN 37013	12
Heads up: addresses aren't normalized — some have full "Nashville, TN ..." suffixes and some don't, and casing varies. If the same physical address appears with two different formats, they're being counted separately. Want me to normalize and recount?

4) Fines

- You want Claude to calculate the fines according to the following rules:
- Every missed trash pick up beyond the 2nd at a given address will result in a fine of $500 for the trash hauler.
- Take these results and create a new sheet in the workbook that contains the trash hauler and the total fine amount.

5) Create a Dashboard

- First, ask Claude how many days are covered in this data?
- Next ask Claude to make a dashboard for you choosing whichever metrics it thinks are more important.
- If Claude provided some rows with a grand total, double check that total.
- What are the good aspects of the final dashboard?
- What are the things that are not good?
- Could this dashboard be a good starting point to improve upon it or would it be better just to create your own from scratch?
