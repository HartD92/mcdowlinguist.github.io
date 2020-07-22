---
layout: post
title:  "Who Signed the Pinker Letter?"

date:   2020-07-22 11:15:00 -0400
tags: linguistics
---

I hate feeling compelled to do this, but here we are. **tl;dr:** I ran some quick 'n dirty stats on the signatories of "the Pinker Letter", and it's not "just graduate students." But also: why are we doing this?

I won't rehash the history of the Pinker letter. I assume if you're reading this, you know what it is, and you know the controversy surrounding it. 

The point of this post is pure and simple. On several occasions, in apparent efforts to discredit "the Letter," Steven Pinker has alluded to the academic status of its signatories. Most recently, on the [BBC radio program](https://www.bbc.co.uk/programmes/m000l0jn){:target="_blank"} "World at One" with Sarah Montague, he claimed, "Most of them were graduate students and lecturers... by no means an indication of the sentiment of professional linguists."

I won't go into the many ways in which I find that statement problematic. I defer to my colleagues for that one (here's [a recent example](https://medium.com/@c.moriah.green/pinker-propaganda-ii-the-re-pinkening-3d1c69e43ab2){:target="_blank"} from Dr. Caitlin Green).

What I want to point out here is that this statement is, to give the benefit of the doubt, an oversimplification. At worst, misleading or disingenuous. As other linguists have [pointed out](https://twitter.com/thai101/status/1285934268942884864){:target="_blank"}, 7 LSA Fellows figure among the signatories of the Letter, and there are definitely professors to be found on the list.

So let's quantify who signed the Letter, to put this to rest once and for all. With reproducible R code (see the very end of the post)! This is a very simple task.

First, let's convert the signatures from the Letter. Note that the data are anonymized here. Otherwise, I pasted the data into the code so you can see the institutions and roles.

I then generated a list of all unique text in the "Role" column and manually classified them as either professor, student, lecturer, researcher or other. I hope I didn't step on any toes with this one. I looked up a couple of ambiguous titles, but most I went with what was written. Again, you can see these categories in the code. Some particularities:

* Visiting professors were counted as professors. 
* Postdoctoral researchers were grouped in with data scientists and so on, unless "teaching" was indicated (in which case, they were counted as a lecturer)
* Alums were counted as students if nothing else was indicated.
* "Other" includes professionals within and outside of linguistics.
* Anyone listing "lecturer" status in the UK, South Korea, Australia or New Zealand was manually changed to "professor," as the title corresponds to Assistant Professor or higher in North America. (This affected 16 peoples' classification.) Lecturers at European institutions were left off this list out of an abundance of caution.

Note that this exercise felt pretty weird to me. Academic rank is a strange thing, and this whole classification scheme felt a little unsavory and demeaning. Anyway. Once those roles are defined, we make a lookup dataframe and match people with their generalized roles. (I reordered the factor to make the bar graph pretty.)

Let's take a look at the values:

* Student: 220
* Professor: 176
* Researcher: 52
* Lecturer: 16
* Other: 44

124 names lacked a title. These were excluded from the graph. If anyone wants to look them up, have fun. 

Here are those results in a bar graph. 

![Why are we doing this](/assets/pinker_letter.png){:style="height:600px;"}

Take from this what you will. Don't @ me.

I want to be crystal clear about one thing: even if the Letter was written *exclusively* by students, that shouldn't discredit their claims *a priori*. A lot of Pinker defenders criticize the Letter and its proponents as levelling *ad hominem* attacks against Pinker -- what is this, if not that? Pinker is using the identities of the Letter signatories as a tactic to invalidate its claims. Those claims should be addressed, rather than nitpicking or attacking an often arbitrary status. (Have you seen the academic job market??)

I'm going to stop there before I go off in a tangent. Again, this post is just to quantify *who* signed the letter, because some people think that matters.

I even hesitated to write this post for fear of giving credence to this kind of argument. But in the end, I wanted to show that, playing by these (harmful!) rules, dismissing the Letter based on the status of the people who signed it is not as easy as, ahem, *certain people* have made it out to be.

* * *

## The code
{% highlight r %}
sign = read.csv2(text = "
name;Science Park, Hong Kong;NLP Engineer
name;University of Michigan;Assistant Professor
name;MIT;PhD student
name;Newcastle University;
name;Harvard University;Postdoctoral Researcher
name;Queen Mary University of London;Professor of Linguistics
name;;
name;;
name;Princeton;Assistant Professor
name;;
name;University of Maryland;
name;University of Oxford;Associate Professor
name;The University of Texas at Austin;
name;University of Massachusetts, Amherst;PhD candidate
name;McMaster University;Associate Professor
name;Yale University;PhD Student
name;Stony Brook University;Lecturer
name;MIT Linguistics;Assistant Professor
name;Johns Hopkins University;PhD student
name;UC San Diego;Graduate Student
name;The University of Chicago;Associate Professor
name;New York University;Associate Professor
name;University of Connecticut;PhD Student
name;University of Michigan;Postdoctoral Research Fellow
name;UC Santa Barbara;PhD Candidate
name;Université de Montréal;Associate Professor
name;The Ohio State University;PhD Candidate
name;;Analytical Engineer
name;Yale University;PhD Candidate
name;CU Boulder;PhD student
name;University of British Columbia;Postdoc
name;University of Massachusetts, Amherst;PhD Student
name;Indiana State University;Assistant Professor
name;University of Wisconsin–Madison;Postdoctoral Researcher
name;New York University;
name;Massachusetts Institute of Technology;PhD candidate
name;;
name;Knology;Researcher
name;Marquette University;Associate Professor
name;Georgetown University;PhD Candidate
name;MIT;PhD Student
name;Washington University in St. Louis;Lecturer
name;The Graduate Center, CUNY;
name;University of Delaware;graduate student
name;Georgetown University;PhD Candidate
name;Life Member, AAAI / Life Member, ACM;NLP Services
name;NYU;Alum
name;Escuela Nacional de Antropología e Historia;Professor
name;Reed College;Associate Professor
name;UMass Amherst;
name;;Fellow, Linguistics Society of America
name;University of Virginia;Postdoctoral Researcher
name;University of Hawai'i at Mānoa;Adjunct Assistant Professor
name;UCLA;
name;Binghamton University;Alum
name;University of Washington, Department of Linguistics;Professor
name;UC Berkeley;Assistant Professor
name;University of California, Santa Cruz;Associate Professor
name;University of Hawai'i at Mānoa Department of Linguistics;Associate Professor
name;Iowa State University;Alum
name;University of Chicago;Assistant Professor
name;University of North Carolina at Asheville;Assistant Professor
name;University of Toronto;PhD Student
name;University of Michigan, Ann Arbor;PhD student
name;Queen’s University;Assistant Professor
name;University of Toronto;
name;Gonville & Caius College, University of Cambridge;
name;New York University;PhD Candidate
name;Rutgers University;PhD Candidate
name;University of Edinburgh;Student
name;University of Göttingen;Postdoctoral researcher
name;Vanderbilt University;Alum
name;Queen Mary University of London;Department chair
name;UC Berkeley;
name;University of Michigan;PhD Candidate
name;;Private sector computational linguist
name;Macquarie University;Research Fellow
name;Yale university;Professor
name;University of Alaska Anchorage;Professor
name;New York University;Assistant Professor
name;Penn State University;Associate Professor of Psychology
name;Stanford;PhD candidate
name;UC Santa Cruz;PhD Student
name;;
name;University of Leeds;
name;New York University;
name;Hoa Sen University;Assistant Professor
name;Calvin University;Affiliate Professor
name;University of North Carolina at Chapel Hill;Adjunct Assistant Professor
name;University of Kentucky;Associate Professor of Linguistics
name;University of Massachusetts Amherst;Associate Professor
name;University of Illinois at Urbana-Champaign;Assistant Professor
name;Ohio State University;
name;Ulster University;PhD Researcher
name;Northern Arizona University;Graduate student
name;University of Michigan;PhD Candidate
name;Virginia Tech;associate professor
name;Cognitive Science B.A.;
name;Southern Illinois University Carbondale;Professor & Chair
name;Stony Brook University;
name;New York University Abu Dhabi;Research Scientist
name;;
name;Stony Brook University;PhD Student
name;University of Virginia;Linguistics MA
name;Boston University;Associate Professor
name;New York University;
name;Rutgers University;Graduate Fellow
name;CU Boulder;PhD student
name;;
name;New York University Department of Communicative Sciences and Disorders;PhD student
name;Queen Mary University of London;Lecturer
name;San Joaquin Delta College;Instructor
name;;
name;;Student
name;McGill University;Student
name;University of Massachusetts Amherst;
name;University of California, San Diego;Assistant Professor
name;University at Albany;Assistant professor
name;California State University, San Bernardino;Graduate Student
name;Stanford University;PhD Student
name;Ohio State University;Professor
name;The Ohio State University;Graduate Student
name;University of Pittsburgh;Faculty Librarian
name;The Ohio State University;PhD Student
name;University of Chicago;PhD Candidate
name;University of Washington;
name;McGill University;Associate Professor
name;The University of Texas at Austin;PhD student
name;University of North Texas;Student
name;;
name;University of Arizona;
name;New York University;Assistant Professor
name;University of Toronto;
name;;
name;Arizona State University;Research Technician
name;University of Michigan;Ph.D Student
name;University of Toronto;PhD candidate
name;UC Santa Barbara;graduate student
name;University of South Carolina;PhD Student
name;University of Edinburgh;Reader
name;;Software Engineer
name;Georgetown University;Phd. Candidate
name;University of Victoria;Professor
name;University of Delaware;Assistant Professor
name;;
name;Monash University Linguistics Society;President
name;Apple, Inc.;Software Engineer
name;;
name;Washington University in St. Louis;Lecturer
name;;
name;NYU;Professor
name;Johns Hopkins University;Postdoctoral Fellow
name;University of Illinois, Urbana-Champaign;Associate Professor
name;Utrecht University;Lecturer
name;University of Utah;Assistant Professor
name;Leiden University;Lecturer
name;University of British Columbia;Associate Professor
name;Santa Fe Community College;Professor
name;Birmingham City University;Education Developer
name;University of Toronto Mississauga;Assistant Professor
name;Yale University;Lector
name;UCLA;Graduate Student
name;University of Nottingham;Assistant Professor
name;University of Nottingham;Visiting Research Fellow
name;The University of Texas at Austin;Postdoctoral Fellow
name;University at Buffalo;Assistant Professor
name;San Diego State University;Assistant Professor
name;Swarthmore College;Visiting Assistant Professor
name;Stony Brook University;Alum
name;University of Maryland;PhD Student
name;University of California, Berkeley;PhD student
name;University of Illinois at Urbana-Champaign;PhD Candidate
name;;
name;MIT;
name;University of California, Berkeley;Graduate student
name;Newcastle University;Lecturer in Sociolinguistics
name;Université du Québec à Montréal (UQAM);Graduate student
name;Boston University;Alum, Linguistics Blogger
name;Charles University, Prague;Assistant Professor
name;University of Hawai'i at Mānoa;Assistant Professor
name;University of Vermont;Associate Professor
name;Massachusetts Institute of Technology;Postdoctoral Associate
name;Princeton University, Program in Linguistics;Postdoctoral Research Associate
name;The University of Texas, Austin;PhD Student
name;UMass Amherst;PhD Student
name;;
name;Simon Fraser University;Associate Professor
name;UCLA;Postdoctoral Fellow
name;New York University Department of Communicative Sciences and Disorders;PhD Student
name;Michigan State University;PhD graduate
name;University of Arizona;
name;Pacific Lutheran University;Associate Professor
name;Coastal Carolina University;Assistant Professor
name;University of Wisconsin-Milwaukee;Associate Professor
name;University of Edinburgh;PhD Student NLP
name;MIT;graduate student
name;University of Georgia;Assistant Professor
name;University of Hawai'i;
name;University of Chicago;Associate Prof.
name;Purdue University;Associate Professor
name;University of Delaware;Assistant Professor
name;University of the Basque Country;PhD Student
name;UPenn;Alum
name;;
name;University of Kentucky;Assistant Professor
name;Utrecht University;Postdoctoral Researcher
name;Monash University;
name;University of Toronto;PhD student
name;University of Chicago;professor
name;Ohio University;Assistant Professor
name;University of North Carolina at Charlotte;Assistant Professor
name;Vanderbilt University;PhD student
name;UC Berkeley;Professor & LSA Fellow
name;UCSB Linguistics;PhD Candidate
name;Swarthmore College;Assistant Professor
name;Dialpad;Speech Recognition Engineer
name;;
name;University of Rochester;Associate Professor
name;NYU;Research Staff
name;Yale University;PhD Candidate
name;CUNY - Hunter College;
name;The University of Texas at Austin;PhD student
name;;
name;;TESL Student
name;The Vocal Fries;Co-host
name;University of Illinois Urbana Champaign;PhD student
name;McGill University;Associate Professor
name;University of Massachusetts, Amherst;Graduate Student
name;Brandeis University;graduate student
name;UC Davis;Graduate student
name;RWTH;
name;University at Buffalo;Professor
name;Graduate Center, City University of New York;
name;University of Texas at Austin;PhD Student Computational Linguistics
name;MIT;PhD student
name;University of Duisburg-Essen;Research Fellow
name;;
name;University of Texas at Austin;
name;Victoria University of Wellington;Research Fellow
name;Google;Program Manager
name;Michigan State University;Graduate student
name;University of Vienna;Assistant Professor
name;The New School;
name;MIT;PhD Student
name;University of Colorado Boulder;PhD student
name;University of Toronto;Alum
name;University of Chicago;
name;City University of New York - College of Staten Island;Assistant Professor
name;University of Manitoba;
name;University of Edinburgh;Reader
name;Saint Mary's University, Halifax, Nova Scotia;associate professor; LSA member
name;University of Minnesota;Associate Professor
name;University of Chicago;PhD Student
name;Yale University;PhD Candidate
name;University of Arizona;Professor
name;University of Southern California;PhD Candidate
name;University of Arizona;
name;University of Göttingen;PhD Candidate
name;;
name;University of Western Ontario;Associate Professor
name;University of Pittsburgh;Director of Undergraduate Studies
name;University of Michigan;Linguistics PhD
name;Medical University of South Carolina;Senior Research Scientist
name;University of Arizona;Associate Professor of Linguistics
name;Western Sydney University, Australia;Associate Professor
name;;
name;University of Maryland;
name;University of Melbourne;
name;University of Massachusetts Amherst;PhD student
name;Queen Mary University of London;Graduate Student
name;University of Texas at Austin;PhD. Candidate
name;University of Massachusetts Amherst;PhD Student
name;CSU Fullerton;MA student
name;University of Delaware;PhD student
name;Achva Academic College;
name;University of California, Santa Barbara;
name;;MA Linguistics
name;University of Toronto;Alum
name;;
name;University of Wisconsin;Postdoctoral Researcher
name;University of Oregon;Postdoctoral Scholar
name;University of Edinburgh;
name;;
name;UC Berkeley;Associate Professor
name;University of Washington;PhD Student
name;University of Kentucky;Alumnus, MA Linguistic Theory and Typology
name;Seoul National University;Assistant professor
name;New York University;PhD Candidate
name;University of Essex;Lecturer
name;;
name;University of Pennsylvania;PhD Graduate
name;The University of Texas at Austin;PhD Student
name;Princeton University;Assistant Professor
name;University of California, Berkeley;PhD Student
name;UW-Madison;Postdoctoral researcher
name;University of Westminster;Assistant Professor
name;University of Edinburgh;
name;University of California, Santa Barbara;Senior Lecturer
name;Reed College;Associate Professor
name;University of Pittsburgh;Professor & Chair
name;University of Kent;Senior lecturer
name;Yale University;Postdoc
name;University of Manchester;Lecturer
name;Google;Senior Linguist
name;University of Saskatchewan;Sessional Lecturer
name;St. Pölten University of Applied Sciences;Researcher
name;;Linguist
name;Tel Aviv University;Graduate Student
name;;
name;University of Toronto;PhD Candidate
name;CU Boulder;Grad Student
name;Stony Brook University;PhD student
name;;Computational Linguist
name;Central Connecticut State University;Associate Professor
name;University of Connecticut;PhD candidate
name;Georgetown University;
name;Gallaudet University;PhD Student
name;UC Santa Cruz;PhD graduate
name;University of Manchester;Undergraduate student
name;;
name;NTNU;Associate Professor
name;University of Edinburgh;
name;Carleton University;PhD Candidate
name;New York University Abu Dhabi;
name;UC Berkeley;PhD Candidate
name;;
name;;
name;;
name;UC Berkeley;Graduate Student
name;;
name;University at Buffalo, SUNY;Graduate Student
name;University of Strasbourg;Postdoctoral Researcher
name;University of Newcastle;Lecturer
name;Google;
name;New York University;PhD student
name;University of Colorado Boulder;PhD student
name;UConn;PhD Student
name;University of California, Riverside;Associate Professor
name;;
name;University of Vienna;student
name;NYU;
name;University of Michigan;Lecturer
name;University of Connecticut;PhD Student
name;Georgia Southern University;Visiting Instructor
name;Jinggangshan University;Research Scientist
name;;
name;The Ohio State University;PhD Student
name;Boston University;
name;University of Maryland;Graduate student
name;Johns Hopkins University;PhD candidate
name;7000 Languages;Executive Director
name;University of Hamburg;Postdoc
name;Macalester College;Visiting Assistant Professor
name;The Graduate Center, City University of New York;PhD student
name;;
name;Stanford University;PhD student
name;University College Dublin;Postdoctoral Fellow
name;George Mason University;Term Assistant Professor
name;Harvard;PhD candidate
name;University of Maryland;PhD student
name;La Trobe University;Graduate student
name;Georgetown University;PhD Candidate
name;New York University;Assistant Professor
name;Princeton University;Undergraduate student
name;UCSC;MA Linguistics graduate
name;UC Berkeley;PhD Candidate
name;Dialpad, Inc.;Computational Linguist
name;Brandeis University;Associate Professor
name;University of Edinburgh;Postdoctoral researcher
name;University of Vermont;Professor and Chair, Department of Anthropology
name;Boston University;Visiting Researcher
name;University of Edinburgh;Postgraduate Student
name;California State University, Northridge;Alumna
name;Georgetown University;PhD Student
name;University of Washington;PhD Candidate
name;University of California, Los Angeles;PhD Candidate
name;McGill University;Grad Student
name;Queen Mary University of London;Senior Lecturer
name;Humboldt-Universität zu Berlin;
name;MIT;Graduate student
name;University of Arizona;Ph.D. Student
name;University of Chicago;Graduate Student
name;Yale University;
name;University of Chicago, English Language Institute;Director
name;University of Pittsburgh;Senior Lecturer
name;Northeastern State University;Assistant Professor
name;;
name;Simon Fraser University;research staff
name;Johns Hopkins University;Graduate student
name;Aoyama Gakuin University;Professor
name;Leibniz-Zentrum Allgemeine Sprachwissenschaft;
name;University of Kentucky;Assistant Professor
name;University of Arizona;
name;Dartmouth College;Associate Professor
name;University of Jyväskylä;University teacher
name;Queen Mary University of London;PhD Candidate
name;;
name;;
name;Lund University;Postdoctoral Researcher
name;University of Michigan;
name;Indiana University;Associate Professor Emeritus
name;Because Language;Co-presenter
name;Stanford University;PhD candidate, Communication
name;SUNY Oswego;Visiting Assistant Professor
name;Western Michigan University;Associate Professor
name;Northwestern University;PhD student
name;Carleton College;
name;;Data Scientist
name;New York University;
name;University of British Columbia;Alum
name;NYU;Postdoc
name;;
name;University of Chicago;Professor of Linguistics
name;University of Minnesota;Professor and Chair
name;University of South Carolina;PhD Student
name;Cornell University;Associate Professor
name;Georgetown University;Alum
name;The University of Edinburgh;PhD candidate
name;Heinrich Heine University;Postdoctoral researcher
name;University of Florida;
name;University of Michigan;Assistant Professor
name;York University Linguistics;Assoc Professor
name;Université du Québec à Montréal (UQAM);MA student
name;Simon Fraser University/University of British Columbia;MA/PhD student
name;University of Calgary;PhD Candidate
name;Stony Brook University;
name;Dartmouth College;Postdoctoral Researcher
name;UQAM;Professor
name;University of Washington;PhD student
name;Google Japan;Computational Linguist
name;University of Connecticut;PhD student
name;Rice University;Associate Professor
name;Oakland University;Associate Professor
name;University of Edinburgh;PhD Candidate
name;Université de Montréal & Université du Québec à Montréal,;course lecturer
name;;
name;;
name;Georgetown University;Associate Professor
name;University of Massachusetts Amherst;Postdoctoral Researcher
name;University of Southern California;
name;Universidad Nacional Autónoma de México;Associate Research Professor
name;York University;PhD student
name;University of Sheffield;Lecturer
name;UC Santa Cruz;Lecturer
name;;
name;University of Toronto;Ph.D. Candidate
name;McGill University;PhD student
name;University of Maryand;
name;New York University;Grad student
name;Department of English and American Studies, Palacký University in Olomouc;Assistant Professor of Linguistics
name;Johns Hopkins University;PhD Student
name;Leibniz-Center for General Linguistics;Postdoctoral Researcher
name;University of Massachusetts Amherst;Professor
name;University of Arizona;PhD Candidate
name;University of Western Ontario;Associate Professor
name;University of Washington;PhD Candidate, Linguistics
name;;
name;University of Cambridge;Student
name;University of Oxford;Associate Professor
name;University of Glasgow;PhD Student
name;Queen Mary University of London;Senior Lecturer
name;University of Massachusetts Boston;PhD student
name;University of Melbourne;Associate Professor
name;University of Washington;Undergraduate
name;University of Toronto;PhD Candidate
name;;
name;McGill University;Emeritus Professor
name;University of Chicago;PhD Candidate
name;Goethe Universität Frankfurt;Postdoctoral researcher
name;University of Texas at Austin;PhD Candidate
name;Brandeis University;Undergraduate Student
name;Morehead State University;Post-doc
name;;
name;San Francisco State University;Assistant Professor
name;University of Maryland;Associate Professor
name;;Linguistics PhD
name;;
name;University of Edinburgh;Teaching Fellow
name;Southern Illinois University Carbondale;Associate Professor & Director of Undergraduate Studies
name;University of Pennsylvania;PhD Candidate
name;West Chester University;Assistant Professor
name;Former LSA Intern;
name;Leipzig University;Postdoctoral Researcher
name;Johns Hopkins University;Associate Professor
name;University of Alabama;Assistant professor
name;University of Edinburgh;Research Fellow
name;UC Davis;Postdoctoral Researcher
name;Concordia University, Montreal;Professor
name;UC Berkeley;PhD Candidate
name;UCLA;Professor and Director of Graduate Studies
name;;PhD student
name;University of Pennsylvania;Postdoctoral Fellow
name;University of Hawai'i at Mānoa;MA Student
name;Carleton University;
name;University of California, Los Angeles;PhD Candidate
name;University of Vermont;Professor and Director
name;NYU;PhD student
name;Loughborough University;Lecturer
name;UC San Diego;PhD Student
name;University at Albany, SUNY;Ph.D. student
name;The Graduate Center, CUNY;Ph.D. Candidate
name;Stanford University;Associate Professor
name;University of Manitoba;Professor
name;CU Boulder;Graduate Student
name;University of California, Berkeley;PhD Candidate
name;;Student
name;Georgetown University;Alum
name;UCLA Linguistics;PhD Candidate
name;McGill University;PhD Student
name;University of California, San Diego;PhD Student
name;Universidade Federal de Belo Horizonte, Brazil;PhD
name;;graduate student
name;NYU;PhD student/worker
name;Michigan State University;Graduate Student
name;University of Gothenburg;Assistant Professor
name;University of Texas at Arlington;Assistant Professor of Instruction
name;Humboldt Universität zu Berlin;Lecturer
name;University of Potsdam;Postdoctoral Researcher
name;Univeristy of Toronto;PhD Student
name;California State University, Fullerton;Associate Professor
name;University of Central Florida;Lecturer
name;CUNY Graduate Center;Presidential Professor
name;Victoria University of Wellington;Senior Lecturer
name;Ohio University;Alum
name;UCSD;PhD candidate
name;The State University of New York at Buffalo;Ph.D. Student
name;Cornell University;Undergraduate Student
name;Indiana University;Associate Professor
name;Truman State University;Professor of Linguistics
name;Yale University;Postbaccalaureate researcher
name;George Mason University;Alum
name;UCSC, UVA;Linguistics MA
name;University of Wisconsin - Madison;Graduate Student
name;;
name;Queen’s University;Associate Professor
name;UC Santa Cruz;Associate Professor
name;University of Virginia;Assistant Professor
name;UCL Institute of Education;PhD student
name;Ohio State University;PhD Candidate
name;Department of Linguistics, University of Chicago;Postdoctoral Teaching Fellow
name;Michigan State University;
name;University of Texas at Austin;Postdoctoral Researcher
name;University of Hawai'i at Mānoa;PhD student
name;University of California Los Angeles;PhD Candidate
name;University of North Texas;
name;University at Buffalo;Professor & Chair
name;;
name;Michigan State University;PhD candidate
name;Michigan State University;Assistant Professor
name;;Postdoctoral Research Fellow
name;Amazon;Applied Scientist
name;University of Texas at Arlington;Ph.D. Candidate
name;California State University Los Angeles.;Professor
name;UChicago;graduate student
name;Hiroshima University;Assistant Professor
name;;
name;University of Toronto;PhD Candidate
name;University of British Columbia;Assistant Professor
name;University of Delaware;PhD Student
name;Bloomsburg University;Assistant Professor
name;Georgetown University;Assistant Professor
name;University of Texas at Austin;
name;;
name;;
name;;Editor
name;American Philosophical Society;Archivist, Linguist
name;New York University;PhD candidate
name;New York University;graduate student
name;CNRS;Postdoctoral researcher
name;Johns Hopkins University;PhD student
name;University of Toronto Mississauga;Assistant Professor
name;The Ohio State University;Alum
name;Northwestern University;PhD Student
name;University of Oxford;
name;The Ohio State University;PhD Student
name;H5/University of California Santa Cruz;Consulting Linguist and PhD alum
name;Florida International University;Professor
name;University of Wisconsin-Madison;Professor
name;New York University;Assistant Professor
name;Boise State University;Associate Professor
name;UC Berkeley;PhD Student
name;University of Missouri-St Louis;Associate professor
name;University of Oslo;MA student
name;University of Toronto;Student
name;McGill University;Professor Emeritus
name;;
name;Newcastle University;Lecturer
name;York University;PhD Candidate
name;University of Illinois at Urbana-Champaign;PhD student
name;Stanford University;Graduate Student
name;Yale University;PhD candidate
name;Long Island University;Associate Professor
name;University of Deusto, Bilbao.;Associate Professor
name;University of Toronto;PhD Candidate
name;University of Stirling;PhD student
name;Appalachian State University;Visiting Assistant Professor
name;Radboud University Nijmegen, The Netherlands;Undergraduate
name;Boise State University;Lecturer
name;University of Cambridge;Undergraduate
name;University of York;Professor
name;University of Tartu;Associate Professor
name;;
name;Sunnyvale School District;Speech-Language Pathologist and Linguistics graduate
name;University of Delaware;Alum
name;University of Konstanz;Professor of Linguistics
name;University of Arizona;Professor and Head
name;Georgetown University;MS Student
name;University of Washington;
name;Swarthmore College;Visiting Assistant Professor, Linguistics
name;Purdue University;PhD student
name;Georgetown University;
name;;
name;;Research Scientist
name;University of Chicago;PhD Student
name;University of Toronto;Graduate Student
name;Pukyong National University;Lecturer
name;York University;PhD Candidate
name;Georgetown University;Alum, BA Linguistics + MS Theoretical Linguistics
name;UQAM;Professor
name;University of Georgia;PhD Student
name;Unaffiliated;Independent Researcher and Consultant
name;Virginia Tech;Alum
name;University of Michigan;PhD Candidate
name;UC Irvine;PhD student in Language Science
name;Boise State University;
name;;Writer
name;University of California, San Diego;Assistant Professor
name;Stanford University;PhD student
name;UC Santa Barbara;Associate Professor of Linguistics
name;;
name;University of York;Lecturer
", header=FALSE)

other = c("NLP Engineer",
          "Analytical Engineer",
          "NLP Services",
          "Alum",
          "Private sector computational linguist",
          "Faculty Librarian",
          "Research Technician",
          "Reader",
          "Software Engineer",
          "Education Developer",
          "Alum, Linguistics Blogger",
          "Speech Recognition Engineer",
          "Co-host",
          "Program Manager",
          "Senior Linguist",
          "Linguist",
          "Computational Linguist",
          "Executive Director",
          "Director",
          "Applied Scientist",
          "Editor",
          "Archivist, Linguist",
          "Consulting Linguist and PhD alum",
          "Speech-Language Pathologist and Linguistics graduate",
          "Writer"
)

prof = c("Assistant Professor",
         "Professor of Linguistics",
         "Associate Professor",
         "Professor",
         "Adjunct Assistant Professor",
         "Department chair",
         "Associate Professor of Psychology",
         "Affiliate Professor",
         "Associate Professor of Linguistics",
         "associate professor",
         "Professor & Chair",
         "Assistant professor",
         "Fellow, Linguistics Society of America", #Beckman
         "Associate Prof.",
         "professor",
         "Professor & LSA Fellow",
         "Term Assistant Professor",
         "Professor and Chair, Department of Anthropology",
         "University teacher",
         "Emeritus Professor",
         "Associate Professor Emeritus",
         "Professor and Chair",
         "Assoc Professor",
         "Associate Research Professor",
         "Assistant Professor of Linguistics",
         "Associate Professor & Director of Undergraduate Studies Professor and Director of Graduate Studies",
         "Professor and Director",
         "Assistant Professor of Instruction",
         "Presidential Professor",
         "Associate professor",
         "Professor Emeritus",
         "Professor and Head",
         "Visiting Assistant Professor, Linguistics"
)

lec = c("Lecturer",
        "Instructor",
        "Lector",
        "Lecturer in Sociolinguistics",
        "Director of Undergraduate Studies", # Heath
        "Senior Lecturer",
        "Senior lecturer",
        "Sessional Lecturer",
        "Visiting Instructor",
        "course lecturer",
        "Teaching Fellow",
        "Postdoctoral Teaching Fellow"
)

stud = c("PhD student",
         "Grad Student",
         "PhD candidate",
         "PhD Student",
         "Graduate Student",
         "PhD Candidate",
         "graduate student",
         "Student",
         "PhD Researcher",
         "Graduate student",
         "Linguistics MA",
         "Graduate Fellow",
         "Ph.D Student",
         "Phd. Candidate",
         "PhD graduate",
         "PhD Student NLP",
         "President", # student president of a Uni linguistics society
         "TESL Student",
         "PhD Student Computational Linguistics",
         "Linguistics PhD",
         "PhD. Candidate",
         "MA student",
         "MA Linguistics",
         "Alumnus, MA Linguistic Theory and Typology",
         "PhD Graduate",
         "Undergraduate student",
         "student",
         "MA Linguistics graduate",
         "Postgraduate Student",
         "Alumna",
         "Ph.D. Student",
         "MA Student",
         "Ph.D. student",
         "PhD",
         "PhD student/worker",
         "MS Student",
         "PhD student in Language Science",
         "Co-presenter",
         "PhD candidate, Communication",
         "MA/PhD student",
         "Ph.D. Candidate",
         "Grad student",
         "PhD Candidate, Linguistics",
         "Undergraduate",
         "Undergraduate Student",
         "Alum, BA Linguistics + MS Theoretical Linguistics"
)

res = c("Postdoctoral Researcher",
        "Postdoctoral Research Fellow",
        "Postdoc",
        "Researcher",
        "Postdoctoral researcher",
        "Research Fellow",
        "Research Scientist",
        "Postdoctoral Fellow",
        "Visiting Research Fellow",
        "Postdoctoral Associate",
        "Postdoctoral Research Associate",
        "Research Staff",
        "Senior Research Scientist",
        "Postdoctoral Scholar",
        "Visiting Researcher",
        "research staff",
        "Data Scientist",
        "Post-doc",
        "Postbaccalaureate researcher",
        "Independent Researcher and Consultant"
)

lookup = data.frame(
  who = c(rep("Lecturer", length(lec)), rep("Other", length(other)), rep("Professor", length(prof)), rep("Researcher", length(res)), rep("Student", length(stud))),
  role = c(lec,other,prof,res,stud)
)

sign$who = lookup$who[match(sign$V3, lookup$role)]

revise = c(111, 156, 161, 176, 290, 302, 304, 379, 334, 462, 444, 499, 524, 588, 617, 632)

sign[revise,]$who = "Professor"

sign = within(sign, who <- factor(who, levels=names(sort(table(who), decreasing=TRUE))))

library(ggplot2)
ggplot(sign[complete.cases(sign$who),], aes(x=who, fill=who)) + 
  geom_bar() +
  geom_text(stat='count', aes(label=..count..), vjust=-1, size=5) +
  theme_classic(base_size = 20) + theme(
  axis.title = element_blank(),
  legend.position = "none",
  plot.title = element_text(hjust = 0.5)
) + scale_y_continuous(limits = c(0, length(which(sign$who=="Student"))+10)) + ggtitle("Who signed the Pinker letter?")
{% endhighlight %}