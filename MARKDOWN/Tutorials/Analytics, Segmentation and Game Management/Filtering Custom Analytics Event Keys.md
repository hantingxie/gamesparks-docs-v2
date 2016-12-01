---
nav_sort: 3
src: /Tutorials/Analytics, Segmentation and Game Management/Filtering Custom Analytics Event Keys.md
---

# Filtering Custom Analytics Event Keys

On a Dynamic Form, you might want to have a chart that shows the extra data attached to the analytics event keys. Specifically, this would be a custom chart driven by data which is not directly accessible through the *NoSQL Explorer*.

Here's how you do this:

*1.* In the portal, go to *Manage > Admin Screens*.

*2.* Under *Screen Builder*, select the *Charts* tab.

![](img/FiltCustAnal/1.png)

In this example, we'll edit the code for an existing Chart called *data*.

*3.* Click the ![](/img/fa/code.png) icon to edit the code for the Chart. The *Chart Builder* appears.

*4.* When you edit the code of the Chart, you'll get some query options instead of the fields for HTML and JavaScript you would get from a normal snippet. If you select *@type* you will see your available analytics keys to the right:

![](img/FiltCustAnal/2.png)

*5.* Then click the *Filter* button and you should see your data options available for the selected analytics event key:

![](img/FiltCustAnal/3.png)

*6.* You can customize your chart and hit *Test* to see the data for that key:

![](img/FiltCustAnal/4.png)

In this example, we've only got one element with a count of 1 returned for the filter we configured for the custom Chart. But this illustrates the steps you need to follow to drive your custom Chart with data attached to analytics event keys!
