# assignment2-Wageman

# Name: Aaron Wageman
### Favorite place to buy food: California Taco Shop

The shop is located just off the **interstate**. There is also a **Popeyes** right next to it. Down the street there is a **Whataburger**. There is also a **car wash down the street**. The shop is backed up by a subdivision.

---

### Directions to the nearest airport from California Taco Shop
1. Get on I-470 N/MO-291 N in Blue Township from Corporal M. E. Webster Memorial Pkwy/E US Hwy 40
2. Head south for 85 feet
3. Turn right toward Fairview Rd in 443 feet
4. Turn right onto Fairview Rd in 148 feet
5. Turn left onto Corporal M. E. Webster Memoriala Pkwy/E US Hwy 40 in 0.5 miles
6. Turn right onto the I-470 N/MO-291/I-70 ramp in .2 miles
7. Merge onto I-470 N/MO-291 N in 0.5 miles
8. Take exit 16C to merge onto I-70 W toward Kansas City for in 13.1 miles 
9. Keep right at the fork to stay on I-70 W, follow signs for Interstate 70 W/Interstate 29 N/Interstate 35 N/US 71 N/St Joseph/Des Moines in .2 miles
10. Keep left to stay on I-70 W in .6 miles
11. Continue onto US-71 N (signs for I-29/I-35 N/Saint Joseph/Des Moines) in .2 miles
12. Continue onto I-29 N/I-35 N/US-71 N in 4.5 miles
13. Keep left at the fork to continue on I-29 N/US-71 N, follow signs for Interstate 29 N/St Joseph in 12.9 miles
14. Take exit 13 toward KCI Airport in .8 miles.

Foods I would recommend from California Taco Shop:
- Chicken Nachos
- Shrimp Nachos
- Queso Cheese Dip
- Chicken Quesadilla
- Steak Quesadilla


### Link to my AboutMe.md

Click the link to go to my **[AboutMe](AboutMe.md)**

---

### Table of Activities

The following table is contains some sports/activities I recommend. It also contains a location where you can participate and the cost of personal equipment. 

|Activity|Location|Cost($)|
|---|---|---:|
|Swimming|Mozingo Lake|20.00|
|Basketball|Student Rec Center|0.00|
|Hiking|Mozingo Lake|100.00|
|Fishing|Mozingo Lake|100.00|

---

### Favorite Quotes

>You must expect great things of yourself before you can do them
*-Michael Jordan*

>If you're going through hell, keep going.
*-Winston Churchill*

---

### Algorithm Code

> Given a set of points in the plane. the convex hull of the set is the smallest convex polygon that contains all the points of it. Using Graham’s scan algorithm, we can find Convex Hull in O(nLogn) time.

Description from <https://www.geeksforgeeks.org/convex-hull-set-2-graham-scan/>

```
struct pt {
    double x, y;
};

int orientation(pt a, pt b, pt c) {
    double v = a.x*(b.y-c.y)+b.x*(c.y-a.y)+c.x*(a.y-b.y);
    if (v < 0) return -1; // clockwise
    if (v > 0) return +1; // counter-clockwise
    return 0;
}

bool cw(pt a, pt b, pt c, bool include_collinear) {
    int o = orientation(a, b, c);
    return o < 0 || (include_collinear && o == 0);
}
bool collinear(pt a, pt b, pt c) { return orientation(a, b, c) == 0; }

void convex_hull(vector<pt>& a, bool include_collinear = false) {
    pt p0 = *min_element(a.begin(), a.end(), [](pt a, pt b) {
        return make_pair(a.y, a.x) < make_pair(b.y, b.x);
    });
    sort(a.begin(), a.end(), [&p0](const pt& a, const pt& b) {
        int o = orientation(p0, a, b);
        if (o == 0)
            return (p0.x-a.x)*(p0.x-a.x) + (p0.y-a.y)*(p0.y-a.y)
                < (p0.x-b.x)*(p0.x-b.x) + (p0.y-b.y)*(p0.y-b.y);
        return o < 0;
    });
    if (include_collinear) {
        int i = (int)a.size()-1;
        while (i >= 0 && collinear(p0, a[i], a.back())) i--;
        reverse(a.begin()+i+1, a.end());
    }

    vector<pt> st;
    for (int i = 0; i < (int)a.size(); i++) {
        while (st.size() > 1 && !cw(st[st.size()-2], st.back(), a[i], include_collinear))
            st.pop_back();
        st.push_back(a[i]);
    }

    a = st;
}
```
Code sourced from: <https://cp-algorithms.com/geometry/convex-hull.html>




