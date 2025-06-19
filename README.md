## SQL Joins
A JOIN clause combines rows from two or more tables based on related column(s) between
them. The SQL language offers many different types of joins. Note that not all types of JOIN
are implemented by the database engines.
- INNER JOIN: Select rows that have matching values in both tables based on the given
columns
- NATURAL JOIN: Similar to INNER JOIN except that there is no need to specify which
columns are used for matching values
- OUTER JOIN: Unlike INNER JOIN, unmatched rows in one or both tables can be
returned. There are LEFT, RIGHT and FULL OUTER JOIN. SQLite only supports LEFT
OUTER JOIN. For LEFT OUTER JOIN, all the records from the left table are included in
the result.
- CROSS JOIN: Return the Cartesian product of the two joined tables, by matching all
the values from the left table with all the values from the right table.

#### Combinations of INNER JOIN


```sql
%%sql
--1)Inner Join via cross join
-- we get the records about students who took the course with course ID ST101, but we also sort the student names in alphabetical order

select *
from Grade , Student
where Grade.course_id = 'ST101' and Student.student_id=Grade.student_id
order by Student.name

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>course_id</th>
      <th>student_id</th>
      <th>final_mark</th>
      <th>student_id.1</th>
      <th>name</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ST101</td>
      <td>201921323</td>
      <td>78</td>
      <td>201921323</td>
      <td>Ava Smith</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ST101</td>
      <td>202003219</td>
      <td>47</td>
      <td>202003219</td>
      <td>Charlie Jones</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ST101</td>
      <td>201985603</td>
      <td>60</td>
      <td>201985603</td>
      <td>Emily Wood</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```sql
%%sql
--2)Inner Join using join
select *
from Student join Grade on Student.student_id = Grade.student_id
where course_id= 'ST101'
order by Student.name;
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>student_id</th>
      <th>name</th>
      <th>year</th>
      <th>course_id</th>
      <th>student_id.1</th>
      <th>final_mark</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>201921323</td>
      <td>Ava Smith</td>
      <td>2</td>
      <td>ST101</td>
      <td>201921323</td>
      <td>78</td>
    </tr>
    <tr>
      <th>1</th>
      <td>202003219</td>
      <td>Charlie Jones</td>
      <td>1</td>
      <td>ST101</td>
      <td>202003219</td>
      <td>47</td>
    </tr>
    <tr>
      <th>2</th>
      <td>201985603</td>
      <td>Emily Wood</td>
      <td>1</td>
      <td>ST101</td>
      <td>201985603</td>
      <td>60</td>
    </tr>
  </tbody>
</table>
</div>



##### Very Clean JOIN Approach
by USING()
You can use USING with:
- INNER JOIN
- LEFT JOIN
- RIGHT JOIN
- FULL OUTER JOIN (if supported by your SQL dialect)


```sql
%%sql
--3)INNER join via USING()
select *
from Student join Grade USING(student_id)
where course_id = 'ST101'
order by Student.name;
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>student_id</th>
      <th>name</th>
      <th>year</th>
      <th>course_id</th>
      <th>final_mark</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>201921323</td>
      <td>Ava Smith</td>
      <td>2</td>
      <td>ST101</td>
      <td>78</td>
    </tr>
    <tr>
      <th>1</th>
      <td>202003219</td>
      <td>Charlie Jones</td>
      <td>1</td>
      <td>ST101</td>
      <td>47</td>
    </tr>
    <tr>
      <th>2</th>
      <td>201985603</td>
      <td>Emily Wood</td>
      <td>1</td>
      <td>ST101</td>
      <td>60</td>
    </tr>
  </tbody>
</table>
</div>




```sql
%%sql
--4) INNER JOIN via NATURAL JOIN
select *
From Student NATURAL JOIN Grade
WHERE course_id= 'ST101'
ORDER BY Student.name;

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>student_id</th>
      <th>name</th>
      <th>year</th>
      <th>course_id</th>
      <th>final_mark</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>201921323</td>
      <td>Ava Smith</td>
      <td>2</td>
      <td>ST101</td>
      <td>78</td>
    </tr>
    <tr>
      <th>1</th>
      <td>202003219</td>
      <td>Charlie Jones</td>
      <td>1</td>
      <td>ST101</td>
      <td>47</td>
    </tr>
    <tr>
      <th>2</th>
      <td>201985603</td>
      <td>Emily Wood</td>
      <td>1</td>
      <td>ST101</td>
      <td>60</td>
    </tr>
  </tbody>
</table>
</div>



#### Combinations of LEFT & RIGHT JOIN



```sql
%%sql
select *
from Student, Grade;
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>student_id</th>
      <th>name</th>
      <th>year</th>
      <th>course_id</th>
      <th>student_id.1</th>
      <th>final_mark</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>201921323</td>
      <td>Ava Smith</td>
      <td>2</td>
      <td>ST101</td>
      <td>201921323</td>
      <td>78</td>
    </tr>
    <tr>
      <th>1</th>
      <td>201921323</td>
      <td>Ava Smith</td>
      <td>2</td>
      <td>ST101</td>
      <td>201985603</td>
      <td>60</td>
    </tr>
    <tr>
      <th>2</th>
      <td>201921323</td>
      <td>Ava Smith</td>
      <td>2</td>
      <td>ST101</td>
      <td>202003219</td>
      <td>47</td>
    </tr>
    <tr>
      <th>3</th>
      <td>201921323</td>
      <td>Ava Smith</td>
      <td>2</td>
      <td>ST115</td>
      <td>201921323</td>
      <td>92</td>
    </tr>
    <tr>
      <th>4</th>
      <td>201921323</td>
      <td>Ava Smith</td>
      <td>2</td>
      <td>ST115</td>
      <td>202003219</td>
      <td>67</td>
    </tr>
    <tr>
      <th>5</th>
      <td>201921323</td>
      <td>Ava Smith</td>
      <td>2</td>
      <td>ST115</td>
      <td>201933222</td>
      <td>88</td>
    </tr>
    <tr>
      <th>6</th>
      <td>201921323</td>
      <td>Ava Smith</td>
      <td>2</td>
      <td>ST207</td>
      <td>201933222</td>
      <td>73</td>
    </tr>
    <tr>
      <th>7</th>
      <td>201921323</td>
      <td>Ava Smith</td>
      <td>2</td>
      <td>ST207</td>
      <td>201875940</td>
      <td>60</td>
    </tr>
    <tr>
      <th>8</th>
      <td>201832220</td>
      <td>Ben Johnson</td>
      <td>3</td>
      <td>ST101</td>
      <td>201921323</td>
      <td>78</td>
    </tr>
    <tr>
      <th>9</th>
      <td>201832220</td>
      <td>Ben Johnson</td>
      <td>3</td>
      <td>ST101</td>
      <td>201985603</td>
      <td>60</td>
    </tr>
    <tr>
      <th>10</th>
      <td>201832220</td>
      <td>Ben Johnson</td>
      <td>3</td>
      <td>ST101</td>
      <td>202003219</td>
      <td>47</td>
    </tr>
    <tr>
      <th>11</th>
      <td>201832220</td>
      <td>Ben Johnson</td>
      <td>3</td>
      <td>ST115</td>
      <td>201921323</td>
      <td>92</td>
    </tr>
    <tr>
      <th>12</th>
      <td>201832220</td>
      <td>Ben Johnson</td>
      <td>3</td>
      <td>ST115</td>
      <td>202003219</td>
      <td>67</td>
    </tr>
    <tr>
      <th>13</th>
      <td>201832220</td>
      <td>Ben Johnson</td>
      <td>3</td>
      <td>ST115</td>
      <td>201933222</td>
      <td>88</td>
    </tr>
    <tr>
      <th>14</th>
      <td>201832220</td>
      <td>Ben Johnson</td>
      <td>3</td>
      <td>ST207</td>
      <td>201933222</td>
      <td>73</td>
    </tr>
    <tr>
      <th>15</th>
      <td>201832220</td>
      <td>Ben Johnson</td>
      <td>3</td>
      <td>ST207</td>
      <td>201875940</td>
      <td>60</td>
    </tr>
    <tr>
      <th>16</th>
      <td>202003219</td>
      <td>Charlie Jones</td>
      <td>1</td>
      <td>ST101</td>
      <td>201921323</td>
      <td>78</td>
    </tr>
    <tr>
      <th>17</th>
      <td>202003219</td>
      <td>Charlie Jones</td>
      <td>1</td>
      <td>ST101</td>
      <td>201985603</td>
      <td>60</td>
    </tr>
    <tr>
      <th>18</th>
      <td>202003219</td>
      <td>Charlie Jones</td>
      <td>1</td>
      <td>ST101</td>
      <td>202003219</td>
      <td>47</td>
    </tr>
    <tr>
      <th>19</th>
      <td>202003219</td>
      <td>Charlie Jones</td>
      <td>1</td>
      <td>ST115</td>
      <td>201921323</td>
      <td>92</td>
    </tr>
    <tr>
      <th>20</th>
      <td>202003219</td>
      <td>Charlie Jones</td>
      <td>1</td>
      <td>ST115</td>
      <td>202003219</td>
      <td>67</td>
    </tr>
    <tr>
      <th>21</th>
      <td>202003219</td>
      <td>Charlie Jones</td>
      <td>1</td>
      <td>ST115</td>
      <td>201933222</td>
      <td>88</td>
    </tr>
    <tr>
      <th>22</th>
      <td>202003219</td>
      <td>Charlie Jones</td>
      <td>1</td>
      <td>ST207</td>
      <td>201933222</td>
      <td>73</td>
    </tr>
    <tr>
      <th>23</th>
      <td>202003219</td>
      <td>Charlie Jones</td>
      <td>1</td>
      <td>ST207</td>
      <td>201875940</td>
      <td>60</td>
    </tr>
    <tr>
      <th>24</th>
      <td>202045234</td>
      <td>Dan Norris</td>
      <td>1</td>
      <td>ST101</td>
      <td>201921323</td>
      <td>78</td>
    </tr>
    <tr>
      <th>25</th>
      <td>202045234</td>
      <td>Dan Norris</td>
      <td>1</td>
      <td>ST101</td>
      <td>201985603</td>
      <td>60</td>
    </tr>
    <tr>
      <th>26</th>
      <td>202045234</td>
      <td>Dan Norris</td>
      <td>1</td>
      <td>ST101</td>
      <td>202003219</td>
      <td>47</td>
    </tr>
    <tr>
      <th>27</th>
      <td>202045234</td>
      <td>Dan Norris</td>
      <td>1</td>
      <td>ST115</td>
      <td>201921323</td>
      <td>92</td>
    </tr>
    <tr>
      <th>28</th>
      <td>202045234</td>
      <td>Dan Norris</td>
      <td>1</td>
      <td>ST115</td>
      <td>202003219</td>
      <td>67</td>
    </tr>
    <tr>
      <th>29</th>
      <td>202045234</td>
      <td>Dan Norris</td>
      <td>1</td>
      <td>ST115</td>
      <td>201933222</td>
      <td>88</td>
    </tr>
    <tr>
      <th>30</th>
      <td>202045234</td>
      <td>Dan Norris</td>
      <td>1</td>
      <td>ST207</td>
      <td>201933222</td>
      <td>73</td>
    </tr>
    <tr>
      <th>31</th>
      <td>202045234</td>
      <td>Dan Norris</td>
      <td>1</td>
      <td>ST207</td>
      <td>201875940</td>
      <td>60</td>
    </tr>
    <tr>
      <th>32</th>
      <td>201985603</td>
      <td>Emily Wood</td>
      <td>1</td>
      <td>ST101</td>
      <td>201921323</td>
      <td>78</td>
    </tr>
    <tr>
      <th>33</th>
      <td>201985603</td>
      <td>Emily Wood</td>
      <td>1</td>
      <td>ST101</td>
      <td>201985603</td>
      <td>60</td>
    </tr>
    <tr>
      <th>34</th>
      <td>201985603</td>
      <td>Emily Wood</td>
      <td>1</td>
      <td>ST101</td>
      <td>202003219</td>
      <td>47</td>
    </tr>
    <tr>
      <th>35</th>
      <td>201985603</td>
      <td>Emily Wood</td>
      <td>1</td>
      <td>ST115</td>
      <td>201921323</td>
      <td>92</td>
    </tr>
    <tr>
      <th>36</th>
      <td>201985603</td>
      <td>Emily Wood</td>
      <td>1</td>
      <td>ST115</td>
      <td>202003219</td>
      <td>67</td>
    </tr>
    <tr>
      <th>37</th>
      <td>201985603</td>
      <td>Emily Wood</td>
      <td>1</td>
      <td>ST115</td>
      <td>201933222</td>
      <td>88</td>
    </tr>
    <tr>
      <th>38</th>
      <td>201985603</td>
      <td>Emily Wood</td>
      <td>1</td>
      <td>ST207</td>
      <td>201933222</td>
      <td>73</td>
    </tr>
    <tr>
      <th>39</th>
      <td>201985603</td>
      <td>Emily Wood</td>
      <td>1</td>
      <td>ST207</td>
      <td>201875940</td>
      <td>60</td>
    </tr>
    <tr>
      <th>40</th>
      <td>201933222</td>
      <td>Freddie Harris</td>
      <td>2</td>
      <td>ST101</td>
      <td>201921323</td>
      <td>78</td>
    </tr>
    <tr>
      <th>41</th>
      <td>201933222</td>
      <td>Freddie Harris</td>
      <td>2</td>
      <td>ST101</td>
      <td>201985603</td>
      <td>60</td>
    </tr>
    <tr>
      <th>42</th>
      <td>201933222</td>
      <td>Freddie Harris</td>
      <td>2</td>
      <td>ST101</td>
      <td>202003219</td>
      <td>47</td>
    </tr>
    <tr>
      <th>43</th>
      <td>201933222</td>
      <td>Freddie Harris</td>
      <td>2</td>
      <td>ST115</td>
      <td>201921323</td>
      <td>92</td>
    </tr>
    <tr>
      <th>44</th>
      <td>201933222</td>
      <td>Freddie Harris</td>
      <td>2</td>
      <td>ST115</td>
      <td>202003219</td>
      <td>67</td>
    </tr>
    <tr>
      <th>45</th>
      <td>201933222</td>
      <td>Freddie Harris</td>
      <td>2</td>
      <td>ST115</td>
      <td>201933222</td>
      <td>88</td>
    </tr>
    <tr>
      <th>46</th>
      <td>201933222</td>
      <td>Freddie Harris</td>
      <td>2</td>
      <td>ST207</td>
      <td>201933222</td>
      <td>73</td>
    </tr>
    <tr>
      <th>47</th>
      <td>201933222</td>
      <td>Freddie Harris</td>
      <td>2</td>
      <td>ST207</td>
      <td>201875940</td>
      <td>60</td>
    </tr>
    <tr>
      <th>48</th>
      <td>201875940</td>
      <td>Grace Clarke</td>
      <td>2</td>
      <td>ST101</td>
      <td>201921323</td>
      <td>78</td>
    </tr>
    <tr>
      <th>49</th>
      <td>201875940</td>
      <td>Grace Clarke</td>
      <td>2</td>
      <td>ST101</td>
      <td>201985603</td>
      <td>60</td>
    </tr>
    <tr>
      <th>50</th>
      <td>201875940</td>
      <td>Grace Clarke</td>
      <td>2</td>
      <td>ST101</td>
      <td>202003219</td>
      <td>47</td>
    </tr>
    <tr>
      <th>51</th>
      <td>201875940</td>
      <td>Grace Clarke</td>
      <td>2</td>
      <td>ST115</td>
      <td>201921323</td>
      <td>92</td>
    </tr>
    <tr>
      <th>52</th>
      <td>201875940</td>
      <td>Grace Clarke</td>
      <td>2</td>
      <td>ST115</td>
      <td>202003219</td>
      <td>67</td>
    </tr>
    <tr>
      <th>53</th>
      <td>201875940</td>
      <td>Grace Clarke</td>
      <td>2</td>
      <td>ST115</td>
      <td>201933222</td>
      <td>88</td>
    </tr>
    <tr>
      <th>54</th>
      <td>201875940</td>
      <td>Grace Clarke</td>
      <td>2</td>
      <td>ST207</td>
      <td>201933222</td>
      <td>73</td>
    </tr>
    <tr>
      <th>55</th>
      <td>201875940</td>
      <td>Grace Clarke</td>
      <td>2</td>
      <td>ST207</td>
      <td>201875940</td>
      <td>60</td>
    </tr>
  </tbody>
</table>
</div>




```sql
%%sql
--This will return the inner join
select *
From Student INNER JOIN Grade USING(student_id)
ORDER BY Student.name;
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>student_id</th>
      <th>name</th>
      <th>year</th>
      <th>course_id</th>
      <th>final_mark</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>201921323</td>
      <td>Ava Smith</td>
      <td>2</td>
      <td>ST101</td>
      <td>78</td>
    </tr>
    <tr>
      <th>1</th>
      <td>201921323</td>
      <td>Ava Smith</td>
      <td>2</td>
      <td>ST115</td>
      <td>92</td>
    </tr>
    <tr>
      <th>2</th>
      <td>202003219</td>
      <td>Charlie Jones</td>
      <td>1</td>
      <td>ST101</td>
      <td>47</td>
    </tr>
    <tr>
      <th>3</th>
      <td>202003219</td>
      <td>Charlie Jones</td>
      <td>1</td>
      <td>ST115</td>
      <td>67</td>
    </tr>
    <tr>
      <th>4</th>
      <td>201985603</td>
      <td>Emily Wood</td>
      <td>1</td>
      <td>ST101</td>
      <td>60</td>
    </tr>
    <tr>
      <th>5</th>
      <td>201933222</td>
      <td>Freddie Harris</td>
      <td>2</td>
      <td>ST115</td>
      <td>88</td>
    </tr>
    <tr>
      <th>6</th>
      <td>201933222</td>
      <td>Freddie Harris</td>
      <td>2</td>
      <td>ST207</td>
      <td>73</td>
    </tr>
    <tr>
      <th>7</th>
      <td>201875940</td>
      <td>Grace Clarke</td>
      <td>2</td>
      <td>ST207</td>
      <td>60</td>
    </tr>
  </tbody>
</table>
</div>




```sql
%%sql
--The ones that are not shown through inner join are extracted using LEFT JOIN
--• All the students from the left table Student are included (including Ben Johnson and Dan Norris)
--• The students with no corresponding record in the right table Grade, have NULL value in attributes course_id and final_mark from Grade

--In other words, all rows in table Student are included in the result set whether there are matching rows in table Grade or not.

SELECT *
FROM Student LEFT JOIN Grade USING(student_id)
order by Student.name;
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>student_id</th>
      <th>name</th>
      <th>year</th>
      <th>course_id</th>
      <th>final_mark</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>202045234</td>
      <td>Dan Norris</td>
      <td>1</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>201921323</td>
      <td>Ava Smith</td>
      <td>2</td>
      <td>ST101</td>
      <td>78.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>201921323</td>
      <td>Ava Smith</td>
      <td>2</td>
      <td>ST115</td>
      <td>92.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>201832220</td>
      <td>Ben Johnson</td>
      <td>3</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>202003219</td>
      <td>Charlie Jones</td>
      <td>1</td>
      <td>ST101</td>
      <td>47.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>202003219</td>
      <td>Charlie Jones</td>
      <td>1</td>
      <td>ST115</td>
      <td>67.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>201985603</td>
      <td>Emily Wood</td>
      <td>1</td>
      <td>ST101</td>
      <td>60.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>201933222</td>
      <td>Freddie Harris</td>
      <td>2</td>
      <td>ST115</td>
      <td>88.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>201933222</td>
      <td>Freddie Harris</td>
      <td>2</td>
      <td>ST207</td>
      <td>73.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>201875940</td>
      <td>Grace Clarke</td>
      <td>2</td>
      <td>ST207</td>
      <td>60.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
import matplotlib.pyplot as plt
import matplotlib.image as mpimg
img = mpimg.imread('LEFT_JOIN.jpg')
plt.imshow(img)
plt.axis('on')  # Hide axes for better visualization
plt.show()
```


    
![png](output_11_0.png)
    



```sql
%%sql
--Cross JOIN
select *
from Student Cross Join Grade
order by Student.name;
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>student_id</th>
      <th>name</th>
      <th>year</th>
      <th>course_id</th>
      <th>student_id.1</th>
      <th>final_mark</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>202045234</td>
      <td>Dan Norris</td>
      <td>1</td>
      <td>ST101</td>
      <td>201921323</td>
      <td>78</td>
    </tr>
    <tr>
      <th>1</th>
      <td>202045234</td>
      <td>Dan Norris</td>
      <td>1</td>
      <td>ST101</td>
      <td>201985603</td>
      <td>60</td>
    </tr>
    <tr>
      <th>2</th>
      <td>202045234</td>
      <td>Dan Norris</td>
      <td>1</td>
      <td>ST101</td>
      <td>202003219</td>
      <td>47</td>
    </tr>
    <tr>
      <th>3</th>
      <td>202045234</td>
      <td>Dan Norris</td>
      <td>1</td>
      <td>ST115</td>
      <td>201921323</td>
      <td>92</td>
    </tr>
    <tr>
      <th>4</th>
      <td>202045234</td>
      <td>Dan Norris</td>
      <td>1</td>
      <td>ST115</td>
      <td>202003219</td>
      <td>67</td>
    </tr>
    <tr>
      <th>5</th>
      <td>202045234</td>
      <td>Dan Norris</td>
      <td>1</td>
      <td>ST115</td>
      <td>201933222</td>
      <td>88</td>
    </tr>
    <tr>
      <th>6</th>
      <td>202045234</td>
      <td>Dan Norris</td>
      <td>1</td>
      <td>ST207</td>
      <td>201933222</td>
      <td>73</td>
    </tr>
    <tr>
      <th>7</th>
      <td>202045234</td>
      <td>Dan Norris</td>
      <td>1</td>
      <td>ST207</td>
      <td>201875940</td>
      <td>60</td>
    </tr>
    <tr>
      <th>8</th>
      <td>201921323</td>
      <td>Ava Smith</td>
      <td>2</td>
      <td>ST101</td>
      <td>201921323</td>
      <td>78</td>
    </tr>
    <tr>
      <th>9</th>
      <td>201921323</td>
      <td>Ava Smith</td>
      <td>2</td>
      <td>ST101</td>
      <td>201985603</td>
      <td>60</td>
    </tr>
    <tr>
      <th>10</th>
      <td>201921323</td>
      <td>Ava Smith</td>
      <td>2</td>
      <td>ST101</td>
      <td>202003219</td>
      <td>47</td>
    </tr>
    <tr>
      <th>11</th>
      <td>201921323</td>
      <td>Ava Smith</td>
      <td>2</td>
      <td>ST115</td>
      <td>201921323</td>
      <td>92</td>
    </tr>
    <tr>
      <th>12</th>
      <td>201921323</td>
      <td>Ava Smith</td>
      <td>2</td>
      <td>ST115</td>
      <td>202003219</td>
      <td>67</td>
    </tr>
    <tr>
      <th>13</th>
      <td>201921323</td>
      <td>Ava Smith</td>
      <td>2</td>
      <td>ST115</td>
      <td>201933222</td>
      <td>88</td>
    </tr>
    <tr>
      <th>14</th>
      <td>201921323</td>
      <td>Ava Smith</td>
      <td>2</td>
      <td>ST207</td>
      <td>201933222</td>
      <td>73</td>
    </tr>
    <tr>
      <th>15</th>
      <td>201921323</td>
      <td>Ava Smith</td>
      <td>2</td>
      <td>ST207</td>
      <td>201875940</td>
      <td>60</td>
    </tr>
    <tr>
      <th>16</th>
      <td>201832220</td>
      <td>Ben Johnson</td>
      <td>3</td>
      <td>ST101</td>
      <td>201921323</td>
      <td>78</td>
    </tr>
    <tr>
      <th>17</th>
      <td>201832220</td>
      <td>Ben Johnson</td>
      <td>3</td>
      <td>ST101</td>
      <td>201985603</td>
      <td>60</td>
    </tr>
    <tr>
      <th>18</th>
      <td>201832220</td>
      <td>Ben Johnson</td>
      <td>3</td>
      <td>ST101</td>
      <td>202003219</td>
      <td>47</td>
    </tr>
    <tr>
      <th>19</th>
      <td>201832220</td>
      <td>Ben Johnson</td>
      <td>3</td>
      <td>ST115</td>
      <td>201921323</td>
      <td>92</td>
    </tr>
    <tr>
      <th>20</th>
      <td>201832220</td>
      <td>Ben Johnson</td>
      <td>3</td>
      <td>ST115</td>
      <td>202003219</td>
      <td>67</td>
    </tr>
    <tr>
      <th>21</th>
      <td>201832220</td>
      <td>Ben Johnson</td>
      <td>3</td>
      <td>ST115</td>
      <td>201933222</td>
      <td>88</td>
    </tr>
    <tr>
      <th>22</th>
      <td>201832220</td>
      <td>Ben Johnson</td>
      <td>3</td>
      <td>ST207</td>
      <td>201933222</td>
      <td>73</td>
    </tr>
    <tr>
      <th>23</th>
      <td>201832220</td>
      <td>Ben Johnson</td>
      <td>3</td>
      <td>ST207</td>
      <td>201875940</td>
      <td>60</td>
    </tr>
    <tr>
      <th>24</th>
      <td>202003219</td>
      <td>Charlie Jones</td>
      <td>1</td>
      <td>ST101</td>
      <td>201921323</td>
      <td>78</td>
    </tr>
    <tr>
      <th>25</th>
      <td>202003219</td>
      <td>Charlie Jones</td>
      <td>1</td>
      <td>ST101</td>
      <td>201985603</td>
      <td>60</td>
    </tr>
    <tr>
      <th>26</th>
      <td>202003219</td>
      <td>Charlie Jones</td>
      <td>1</td>
      <td>ST101</td>
      <td>202003219</td>
      <td>47</td>
    </tr>
    <tr>
      <th>27</th>
      <td>202003219</td>
      <td>Charlie Jones</td>
      <td>1</td>
      <td>ST115</td>
      <td>201921323</td>
      <td>92</td>
    </tr>
    <tr>
      <th>28</th>
      <td>202003219</td>
      <td>Charlie Jones</td>
      <td>1</td>
      <td>ST115</td>
      <td>202003219</td>
      <td>67</td>
    </tr>
    <tr>
      <th>29</th>
      <td>202003219</td>
      <td>Charlie Jones</td>
      <td>1</td>
      <td>ST115</td>
      <td>201933222</td>
      <td>88</td>
    </tr>
    <tr>
      <th>30</th>
      <td>202003219</td>
      <td>Charlie Jones</td>
      <td>1</td>
      <td>ST207</td>
      <td>201933222</td>
      <td>73</td>
    </tr>
    <tr>
      <th>31</th>
      <td>202003219</td>
      <td>Charlie Jones</td>
      <td>1</td>
      <td>ST207</td>
      <td>201875940</td>
      <td>60</td>
    </tr>
    <tr>
      <th>32</th>
      <td>201985603</td>
      <td>Emily Wood</td>
      <td>1</td>
      <td>ST101</td>
      <td>201921323</td>
      <td>78</td>
    </tr>
    <tr>
      <th>33</th>
      <td>201985603</td>
      <td>Emily Wood</td>
      <td>1</td>
      <td>ST101</td>
      <td>201985603</td>
      <td>60</td>
    </tr>
    <tr>
      <th>34</th>
      <td>201985603</td>
      <td>Emily Wood</td>
      <td>1</td>
      <td>ST101</td>
      <td>202003219</td>
      <td>47</td>
    </tr>
    <tr>
      <th>35</th>
      <td>201985603</td>
      <td>Emily Wood</td>
      <td>1</td>
      <td>ST115</td>
      <td>201921323</td>
      <td>92</td>
    </tr>
    <tr>
      <th>36</th>
      <td>201985603</td>
      <td>Emily Wood</td>
      <td>1</td>
      <td>ST115</td>
      <td>202003219</td>
      <td>67</td>
    </tr>
    <tr>
      <th>37</th>
      <td>201985603</td>
      <td>Emily Wood</td>
      <td>1</td>
      <td>ST115</td>
      <td>201933222</td>
      <td>88</td>
    </tr>
    <tr>
      <th>38</th>
      <td>201985603</td>
      <td>Emily Wood</td>
      <td>1</td>
      <td>ST207</td>
      <td>201933222</td>
      <td>73</td>
    </tr>
    <tr>
      <th>39</th>
      <td>201985603</td>
      <td>Emily Wood</td>
      <td>1</td>
      <td>ST207</td>
      <td>201875940</td>
      <td>60</td>
    </tr>
    <tr>
      <th>40</th>
      <td>201933222</td>
      <td>Freddie Harris</td>
      <td>2</td>
      <td>ST101</td>
      <td>201921323</td>
      <td>78</td>
    </tr>
    <tr>
      <th>41</th>
      <td>201933222</td>
      <td>Freddie Harris</td>
      <td>2</td>
      <td>ST101</td>
      <td>201985603</td>
      <td>60</td>
    </tr>
    <tr>
      <th>42</th>
      <td>201933222</td>
      <td>Freddie Harris</td>
      <td>2</td>
      <td>ST101</td>
      <td>202003219</td>
      <td>47</td>
    </tr>
    <tr>
      <th>43</th>
      <td>201933222</td>
      <td>Freddie Harris</td>
      <td>2</td>
      <td>ST115</td>
      <td>201921323</td>
      <td>92</td>
    </tr>
    <tr>
      <th>44</th>
      <td>201933222</td>
      <td>Freddie Harris</td>
      <td>2</td>
      <td>ST115</td>
      <td>202003219</td>
      <td>67</td>
    </tr>
    <tr>
      <th>45</th>
      <td>201933222</td>
      <td>Freddie Harris</td>
      <td>2</td>
      <td>ST115</td>
      <td>201933222</td>
      <td>88</td>
    </tr>
    <tr>
      <th>46</th>
      <td>201933222</td>
      <td>Freddie Harris</td>
      <td>2</td>
      <td>ST207</td>
      <td>201933222</td>
      <td>73</td>
    </tr>
    <tr>
      <th>47</th>
      <td>201933222</td>
      <td>Freddie Harris</td>
      <td>2</td>
      <td>ST207</td>
      <td>201875940</td>
      <td>60</td>
    </tr>
    <tr>
      <th>48</th>
      <td>201875940</td>
      <td>Grace Clarke</td>
      <td>2</td>
      <td>ST101</td>
      <td>201921323</td>
      <td>78</td>
    </tr>
    <tr>
      <th>49</th>
      <td>201875940</td>
      <td>Grace Clarke</td>
      <td>2</td>
      <td>ST101</td>
      <td>201985603</td>
      <td>60</td>
    </tr>
    <tr>
      <th>50</th>
      <td>201875940</td>
      <td>Grace Clarke</td>
      <td>2</td>
      <td>ST101</td>
      <td>202003219</td>
      <td>47</td>
    </tr>
    <tr>
      <th>51</th>
      <td>201875940</td>
      <td>Grace Clarke</td>
      <td>2</td>
      <td>ST115</td>
      <td>201921323</td>
      <td>92</td>
    </tr>
    <tr>
      <th>52</th>
      <td>201875940</td>
      <td>Grace Clarke</td>
      <td>2</td>
      <td>ST115</td>
      <td>202003219</td>
      <td>67</td>
    </tr>
    <tr>
      <th>53</th>
      <td>201875940</td>
      <td>Grace Clarke</td>
      <td>2</td>
      <td>ST115</td>
      <td>201933222</td>
      <td>88</td>
    </tr>
    <tr>
      <th>54</th>
      <td>201875940</td>
      <td>Grace Clarke</td>
      <td>2</td>
      <td>ST207</td>
      <td>201933222</td>
      <td>73</td>
    </tr>
    <tr>
      <th>55</th>
      <td>201875940</td>
      <td>Grace Clarke</td>
      <td>2</td>
      <td>ST207</td>
      <td>201875940</td>
      <td>60</td>
    </tr>
  </tbody>
</table>
</div>



## Using Python to create and manipulate databases


```python
#connecting to DB using Python
import os
try:
    os.remove('University.db')
except OSError:
    pass
#make sure we run the notebook multiple times without errors
#prepares a SQLite database file for use and is a cleanup step. It ensures that if you're running the notebook or script multiple times (e.g., during development or testing), you start with a fresh database file each time
```


```python
import sqlite3
conn = sqlite3.connect('University.db')
```


```python
#creating tables using python
import pandas as pd

```


```python
student = pd.read_csv('student.csv')
```


```python
course = pd.read_csv('course.csv')
```


```python
grade = pd.read_csv('grade.csv')
```


```python
# write record stored in dataframes as tables to the database university.db using to_Sql()
# index = false to ensure the DF row index is not written into the SQL tables

student.to_sql('student', con = conn, index= False, if_exists='replace')
course.to_sql('course', con = conn, index= False, if_exists='replace')
grade.to_sql('grade', con = conn, index= False, if_exists='replace')
```




    8




```python
#manipulate DB using Python
#first create a cursor object
c = conn.cursor()
```


```python
# execute()	Runs a SQL command and stores it
# fetchall() Retrieves all rows from a result
```


```python
c.execute('''
Select name
from sqlite_master
where type='table'
''')
```




    <sqlite3.Cursor at 0x1c389d142c0>




```python
c.fetchall()
```




    [('student',), ('course',), ('grade',)]




```python
#we can browse each table using pandas
q = c.execute("select * from student").fetchall()
pd.DataFrame(q)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>201921323</td>
      <td>Ava Smith</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>201832220</td>
      <td>Ben Johnson</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>202003219</td>
      <td>Charlie Jones</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>202045234</td>
      <td>Dan Norris</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>201985603</td>
      <td>Emily Wood</td>
      <td>1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>201933222</td>
      <td>Freddie Harris</td>
      <td>2</td>
    </tr>
    <tr>
      <th>6</th>
      <td>201875940</td>
      <td>Grace Clarke</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
#we can add another table to the DB using
c.execute('''
create table Teacher (staff_id TEXT PRIMARY KEY, name TEXT)
''')

```




    <sqlite3.Cursor at 0x1c389d142c0>




```python
conn.commit() #Saves the changes
```


```python
c.execute('''
select name
from sqlite_master
where type='table'
''').fetchall()
```




    [('student',), ('course',), ('grade',), ('Teacher',)]




```python
#Delete a Table
c.execute("DROP TABLE Teacher")
```




    <sqlite3.Cursor at 0x1c389d142c0>




```python
conn.commit()
```


```python
c.execute('''
select name
from sqlite_master
where type='table'
''').fetchall()
```




    [('student',), ('course',), ('grade',)]




```python
#insert a tuple or row
c.execute("Insert into Student values(202029744,'Harper Taylor',1);")
```




    <sqlite3.Cursor at 0x1c389d142c0>




```python

conn.commit()
```


```python
#broswe the table
q = c.execute("select * from Student").fetchall()
pd.DataFrame(q)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>201921323</td>
      <td>Ava Smith</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>201832220</td>
      <td>Ben Johnson</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>202003219</td>
      <td>Charlie Jones</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>202045234</td>
      <td>Dan Norris</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>201985603</td>
      <td>Emily Wood</td>
      <td>1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>201933222</td>
      <td>Freddie Harris</td>
      <td>2</td>
    </tr>
    <tr>
      <th>6</th>
      <td>201875940</td>
      <td>Grace Clarke</td>
      <td>2</td>
    </tr>
    <tr>
      <th>7</th>
      <td>202029744</td>
      <td>Harper Taylor</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
#update a row
c.execute('''
update Student
set student_id = '201929744'
where name = 'Harper Taylor'
''')
```




    <sqlite3.Cursor at 0x1c389d142c0>




```python
conn.commit()
```


```python
q = c.execute("select * from Student").fetchall()
pd.DataFrame(q)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>201921323</td>
      <td>Ava Smith</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>201832220</td>
      <td>Ben Johnson</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>202003219</td>
      <td>Charlie Jones</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>202045234</td>
      <td>Dan Norris</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>201985603</td>
      <td>Emily Wood</td>
      <td>1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>201933222</td>
      <td>Freddie Harris</td>
      <td>2</td>
    </tr>
    <tr>
      <th>6</th>
      <td>201875940</td>
      <td>Grace Clarke</td>
      <td>2</td>
    </tr>
    <tr>
      <th>7</th>
      <td>201929744</td>
      <td>Harper Taylor</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
#delete  a row
c.execute('''
delete from student
where name = 'Harper Taylor'
''')
```




    <sqlite3.Cursor at 0x1c389d142c0>




```python
conn.commit()
```


```python
q = c.execute("select * from Student").fetchall()
pd.DataFrame(q)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>201921323</td>
      <td>Ava Smith</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>201832220</td>
      <td>Ben Johnson</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>202003219</td>
      <td>Charlie Jones</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>202045234</td>
      <td>Dan Norris</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>201985603</td>
      <td>Emily Wood</td>
      <td>1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>201933222</td>
      <td>Freddie Harris</td>
      <td>2</td>
    </tr>
    <tr>
      <th>6</th>
      <td>201875940</td>
      <td>Grace Clarke</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
conn.close()
```


```python
import sqlite3
```


```python
conn1 = sqlite3.connect('University.db')
```


```python
c1=conn1.cursor()
```


```python
c1.execute("select name from sqlite_master where type='table'").fetchall()
```




    [('student',), ('course',), ('grade',)]




```python
#Example 1: get grades of the course 'course_id ST101'

q2 = c1.execute('''
Select final_mark
 from grade
Where course_id = 'ST101'
''').fetchall()

pd.DataFrame(q2)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>78</td>
    </tr>
    <tr>
      <th>1</th>
      <td>60</td>
    </tr>
    <tr>
      <th>2</th>
      <td>47</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Example 2: Get names of students in alpha order
q3 = c1.execute('''
Select Student.name
from Grade, Student
where Grade.course_id = 'ST101' and Student.student_id = Grade.student_id
order by name
''').fetchall()

pd.DataFrame(q3)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Ava Smith</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Charlie Jones</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Emily Wood</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Example 3: Get courses taken by Ava Smith or Freddie Harris

q4 = c1.execute('''
Select DISTINCT course.name
from grade , student , course
where (student.name = 'Ava Smith' OR student.name = 'Freddie Harris') AND student.student_id = grade.student_id AND course.course_id=grade.course_id
''').fetchall()

pd.DataFrame(q4)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>programming for data science</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Managing and Visualising Data</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Databases</td>
    </tr>
  </tbody>
</table>
</div>



### Inspecting and solving the issue of the course table structure by applying if exists = replace


```python
# inspect the schema
tables = c1.execute("SELECT name FROM sqlite_master WHERE type='table'").fetchall()

# Loop through each table and print its schema
for table_name in tables:
    table = table_name[0]

    print(f"\nSchema for table: {table}")
    schema = c1.execute(f"PRAGMA table_info({table})").fetchall()
    for column in schema:
        print(column)

```

    
    Schema for table: student
    (0, 'student_id', 'INTEGER', 0, None, 0)
    (1, 'name', 'TEXT', 0, None, 0)
    (2, 'year', 'INTEGER', 0, None, 0)
    
    Schema for table: course
    (0, 'course_id', 'TEXT', 0, None, 0)
    (1, 'name', 'TEXT', 0, None, 0)
    (2, 'capacity', 'INTEGER', 0, None, 0)
    
    Schema for table: grade
    (0, 'course_id', 'TEXT', 0, None, 0)
    (1, 'student_id', 'INTEGER', 0, None, 0)
    (2, 'final_mark', 'INTEGER', 0, None, 0)
    


```python
q5 = c1.execute('''
Select * from course;
''')

pd.DataFrame(q5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ST101</td>
      <td>programming for data science</td>
      <td>60</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ST115</td>
      <td>Managing and Visualising Data</td>
      <td>60</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ST207</td>
      <td>Databases</td>
      <td>30</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ST310</td>
      <td>Machine Learning</td>
      <td>100</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Example 4: Calculate the AVG mark for each course

q6 = c1.execute('''
Select course_id ,round(avg(final_mark),3) from grade
group by course_id;

''').fetchall()
pd.DataFrame(q6)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ST101</td>
      <td>61.667</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ST115</td>
      <td>82.333</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ST207</td>
      <td>66.500</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
