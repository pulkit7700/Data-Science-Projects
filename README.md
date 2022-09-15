
# Data Science Projects 

This Repository Consists of all the Machine Learning Projects, covring over different type of dataset mentioned below


## Balanced Scale Dataset

| Data Set Characteristics:    | Multivariate   | Number of Instances:  | 625 | Area:               | Social     |
|------------------------------|----------------|-----------------------|-----|---------------------|------------|
| Attribute Characteristics:   | Categorical    | Number of Attributes: | 4   | Date Donated        | 1994-04-22 |
| Associated Tasks:            | Classification | Missing Values?       | No  | Number of Web Hits: | 318570     |
| Highest Percentage Achieved: | N/A            |

 (a) Source: Generated to model psychological experiments reported
		by Siegler, R. S. (1976).  Three Aspects of Cognitive
		Development.  Cognitive Psychology, 8, 481-520.
    (b) Donor: Tim Hume (hume@ics.uci.edu)
    (c) Date: 22 April 1994

3. Past Usage: (possibly different formats of this data)
   - Publications
	1. Klahr, D., & Siegler, R.S. (1978).  The Representation of
	   Children's Knowledge.  In H. W. Reese & L. P. Lipsitt (Eds.),
	   Advances in Child Development and Behavior, pp. 61-116.  New
	   York: Academic Press 
	2. Langley,P. (1987).  A General Theory of Discrimination
	   Learning.  In D. Klahr, P. Langley, & R. Neches (Eds.),
	   Production System Models of Learning and Development, pp.
	   99-161. Cambridge, MA: MIT Press
	3. Newell, A. (1990).  Unified Theories of Cognition.
	   Cambridge, MA: Harvard University Press
	4. McClelland, J.L. (1988).  Parallel Distibuted Processing:
	   Implications for Cognition and Development.  Technical
	   Report AIP-47, Department of Psychology, Carnegie-Mellon
	   University 
	5. Shultz, T., Mareschal, D., & Schmidt, W. (1994).  Modeling
	   Cognitive Development on Balance Scale Phenomena. Machine
	   Learning, Vol. 16, pp. 59-88.

4. Relevant Information: 
	This data set was generated to model psychological
	experimental results.  Each example is classified as having the
	balance scale tip to the right, tip to the left, or be
	balanced.  The attributes are the left weight, the left
	distance, the right weight, and the right distance.  The
	correct way to find the class is the greater of 
	(left-distance * left-weight) and (right-distance *
	right-weight).  If they are equal, it is balanced.

5. Number of Instances: 625 (49 balanced, 288 left, 288 right)

6. Number of Attributes: 4 (numeric) + class name = 5

7. Attribute Information:
	1. Class Name: 3 (L, B, R)
	2. Left-Weight: 5 (1, 2, 3, 4, 5)
	3. Left-Distance: 5 (1, 2, 3, 4, 5)
	4. Right-Weight: 5 (1, 2, 3, 4, 5)
	5. Right-Distance: 5 (1, 2, 3, 4, 5)

8. Missing Attribute Values: 
	none

9. Class Distribution: 
   1. 46.08 percent are L
   2. 07.84 percent are B
   3. 46.08 percent are R
## Breast Cancer Classification Problem  

1. Title: Breast cancer data (Michalski has used this)

2. Sources: 
   -- Matjaz Zwitter & Milan Soklic (physicians)
      Institute of Oncology 
      University Medical Center
      Ljubljana, Yugoslavia
   -- Donors: Ming Tan and Jeff Schlimmer (Jeffrey.Schlimmer@a.gp.cs.cmu.edu)
   -- Date: 11 July 1988

3. Past Usage: (Several: here are some)
     -- Michalski,R.S., Mozetic,I., Hong,J., & Lavrac,N. (1986). The 
        Multi-Purpose Incremental Learning System AQ15 and its Testing 
        Application to Three Medical Domains.  In Proceedings of the 
        Fifth National Conference on Artificial Intelligence, 1041-1045,
        Philadelphia, PA: Morgan Kaufmann.
        -- accuracy range: 66%-72%
     -- Clark,P. & Niblett,T. (1987). Induction in Noisy Domains.  In 
        Progress in Machine Learning (from the Proceedings of the 2nd
        European Working Session on Learning), 11-30, Bled, 
        Yugoslavia: Sigma Press.
        -- 8 test results given: 65%-72% accuracy range
     -- Tan, M., & Eshelman, L. (1988). Using weighted networks to 
        represent classification knowledge in noisy domains.  Proceedings 
        of the Fifth International Conference on Machine Learning, 121-134,
        Ann Arbor, MI.
        -- 4 systems tested: accuracy range was 68%-73.5%
    -- Cestnik,G., Konenenko,I, & Bratko,I. (1987). Assistant-86: A
       Knowledge-Elicitation Tool for Sophisticated Users.  In I.Bratko
       & N.Lavrac (Eds.) Progress in Machine Learning, 31-45, Sigma Press.
       -- Assistant-86: 78% accuracy

4. Relevant Information:
     This is one of three domains provided by the Oncology Institute
     that has repeatedly appeared in the machine learning literature.
     (See also lymphography and primary-tumor.)

     This data set includes 201 instances of one class and 85 instances of
     another class.  The instances are described by 9 attributes, some of
     which are linear and some are nominal.

5. Number of Instances: 286

6. Number of Attributes: 9 + the class attribute

7. Attribute Information:
   1. Class: no-recurrence-events, recurrence-events
   2. age: 10-19, 20-29, 30-39, 40-49, 50-59, 60-69, 70-79, 80-89, 90-99.
   3. menopause: lt40, ge40, premeno.
   4. tumor-size: 0-4, 5-9, 10-14, 15-19, 20-24, 25-29, 30-34, 35-39, 40-44,
                  45-49, 50-54, 55-59.
   5. inv-nodes: 0-2, 3-5, 6-8, 9-11, 12-14, 15-17, 18-20, 21-23, 24-26,
                 27-29, 30-32, 33-35, 36-39.
   6. node-caps: yes, no.
   7. deg-malig: 1, 2, 3.
   8. breast: left, right.
   9. breast-quad: left-up, left-low, right-up,	right-low, central.
  10. irradiat:	yes, no.

8. Missing Attribute Values: (denoted by "?")
   Attribute #:  Number of instances with missing values:
   6.             8
   9.             1.

9. Class Distribution:
    1. no-recurrence-events: 201 instances
    2. recurrence-events: 85 instances
## Car Value Prediction 

| Data Set Characteristics:    | Multivariate   | Number of Instances:  | 1728 | Area:               | N/A        |
|------------------------------|----------------|-----------------------|------|---------------------|------------|
| Attribute Characteristics:   | Categorical    | Number of Attributes: | 6    | Date Donated        | 1997-06-01 |
| Associated Tasks:            | Classification | Missing Values?       | No   | Number of Web Hits: | 1618076    |
| Highest Percentage Achieved: | N/A            |                       |      |                     |            |


1. Title: Car Evaluation Database

2. Sources:
   (a) Creator: Marko Bohanec
   (b) Donors: Marko Bohanec   (marko.bohanec@ijs.si)
               Blaz Zupan      (blaz.zupan@ijs.si)
   (c) Date: June, 1997

3. Past Usage:

   The hierarchical decision model, from which this dataset is
   derived, was first presented in 

   M. Bohanec and V. Rajkovic: Knowledge acquisition and explanation for
   multi-attribute decision making. In 8th Intl Workshop on Expert
   Systems and their Applications, Avignon, France. pages 59-78, 1988.

   Within machine-learning, this dataset was used for the evaluation
   of HINT (Hierarchy INduction Tool), which was proved to be able to
   completely reconstruct the original hierarchical model. This,
   together with a comparison with C4.5, is presented in

   B. Zupan, M. Bohanec, I. Bratko, J. Demsar: Machine learning by
   function decomposition. ICML-97, Nashville, TN. 1997 (to appear)

4. Relevant Information Paragraph:

   Car Evaluation Database was derived from a simple hierarchical
   decision model originally developed for the demonstration of DEX
   (M. Bohanec, V. Rajkovic: Expert system for decision
   making. Sistemica 1(1), pp. 145-157, 1990.). The model evaluates
   cars according to the following concept structure:

   CAR                      car acceptability
   . PRICE                  overall price
   . . buying               buying price
   . . maint                price of the maintenance
   . TECH                   technical characteristics
   . . COMFORT              comfort
   . . . doors              number of doors
   . . . persons            capacity in terms of persons to carry
   . . . lug_boot           the size of luggage boot
   . . safety               estimated safety of the car

   Input attributes are printed in lowercase. Besides the target
   concept (CAR), the model includes three intermediate concepts:
   PRICE, TECH, COMFORT. Every concept is in the original model
   related to its lower level descendants by a set of examples (for
   these examples sets see http://www-ai.ijs.si/BlazZupan/car.html).

   The Car Evaluation Database contains examples with the structural
   information removed, i.e., directly relates CAR to the six input
   attributes: buying, maint, doors, persons, lug_boot, safety.

   Because of known underlying concept structure, this database may be
   particularly useful for testing constructive induction and
   structure discovery methods.

5. Number of Instances: 1728
   (instances completely cover the attribute space)

6. Number of Attributes: 6

7. Attribute Values:

   buying       v-high, high, med, low
   maint        v-high, high, med, low
   doors        2, 3, 4, 5-more
   persons      2, 4, more
   lug_boot     small, med, big
   safety       low, med, high

8. Missing Attribute Values: none

9. Class Distribution (number of instances per class)

  | Class      | N |   N[%]      |
| ----------- | ----------- | -----  | 
| Unacc      | 1210       |  70.023 |
| acc   | 384        |  22.222 |
| Good     | 69       | 3.993  |
| V-Good   | 65        |  3.762 |
