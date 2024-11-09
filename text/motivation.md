---
id: motivation
aliases: []
tags: []
---

The motivation to develop such tool was first felt during the first semester of my studies. Arguably the most difficult semester requires you to juggle between three time demanding courses, namely
TODO: IB111 - Introduction to programming, IB015 - Non-imperative progamming and IB000 - Basic math something. On top of these there are couple more courses whose difficulty also cannot be
underestimated. Moreover, for the vast majority of students, this is the first time they experience the fast-paced life of an university student, which is a major factor in one's succes in the
first semester. 

Being focused on the main three courses, I have inadvertyl underestimated and neglect the remaing courses of that semester. Having the concious urge to balance my time among all these responsibilities,
I needed to know how much time I spend on each one of them. I felt like I could not spend any more time studying; however, as the saying goes: 'Measure before optimizing.' And measure I did.

The very first iteration of this tool, lets say iteration 0, was a simple, barebone python CLI application. It accepted three arguments - starting time, ending time and category.
The fist two are self explanatory, the `category` argument was just name of the course or subject, e.i and example of one such 'entry' would be:

```json
{
    "startTime": "2022-09-27 18:00:00.000",
    "endTime": "2022-09-27 20:00:00.000",
    "category": "IB111"
}
```
These entries would get persited into a big JSON file, hence the JSON format. A slight improvement was an integration with a charting library `matplotlib`, which I used to create a simple 
pie chart of all the date, grouped by `category` resulting in the following:
![[nowaster_graph.png]]

This covered the simple usecase I was going for. However, more requirements started to come up:
- sync across multiple devices
I wanted this data to be synced across multiple devices, such that when I work on a faculty computer, I can also view and create addition entries. Not to mention the need to access this application
on a mobile phone
- better user experience
The user experience was, at best, clunky. CLI applications surely have their place, but this was starting to grow a bit bigger, and a better UX was needed
- filtering
A crucial feature when it comes to time-management is filtering the entries. A very simple, yet frequent question might be "How much time have i spent on IB111 over the weekend?". This query
sounds trivial, just filter the entries between two dates where the category is equal to IB111, and it indeed is trivial. However the current UI does not support filtering of any kind.
- security
If I were to expose this application publicly, and cover point 1 by doing so, I would allow anyone and everyone to read and edit my personal data. This is obviously not desired, thefore some kind
of authentication flow is required
- tagging
The application should allow adding arbitrary tags to an entry. A tag may be viewed as a subcategory, which further devides given session. These tags can be used to increase granularity of 
which time is managed. An example entries with tags may look like this

```json
{
    "startTime": "2022-09-27 18:00:00.000",
    "endTime": "2022-09-27 20:00:00.000",
    "category": "IB111",
    "tags": ["homework-02"]
}
{
    "startTime": "2022-09-27 18:00:00.000",
    "endTime": "2022-09-27 20:00:00.000",
    "category": "IB111",
    "tags": ["seminar", "recursion"]
}
```
This should allow the user to get deeper insight into the time spent within a category.

The aforementioned requirements add non-trivial complexity to the application. Such complexity is difficult to implement, and since "one should not reinvent the wheel", we first need to 
research already existing products, which is what the next chapter entails.
