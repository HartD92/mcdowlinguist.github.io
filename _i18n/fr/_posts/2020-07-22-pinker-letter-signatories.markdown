---
layout: post
title:  "Who Signed the Pinker Letter?"

date:   2020-07-22 11:15:00 -0400
tags: linguistics
---

I hate feeling compelled to do this, but here we are. tl;dr: I ran some quick 'n dirty stats on the signatories of "the Pinker Letter", and it's not "just graduate students." But also: why are we doing this?

I won't rehash the history of the Pinker letter. I assume if you're reading this, you know what it is, and you know the controversy surrounding it. 

The point of this post is pure and simple. On several occasions, in apparent efforts to discredit "the Letter," Steven Pinker has alluded to the academic status of its signatories. Most recently, on the BBC radio program "World at One" with Sarah Montague, he claimed "Most of them were graduate students and lecturers... by no means an indication of the sentiment of professional linguists."

I won't go into the many ways in which I find that statement problematic. I defer to my colleagues for that one (here's [a recent example](https://medium.com/@c.moriah.green/pinker-propaganda-ii-the-re-pinkening-3d1c69e43ab2){:target="_blank"} from Dr. Caitlin Green).

What I want to point out here is that this statement is, to give the benefit of the doubt, an oversimplification. At worst, misleading or disingenuous. As other linguists have [pointed out](https://twitter.com/thai101/status/1285934268942884864){:target="_blank"}, 7 LSA Fellows figure among the signatories of the Letter, and there are definitely professors to be found on the list.

So let's quantify who signed the Letter, to put this to rest once and for all. With reproducible R code (see the very end of the post)! This is a very simple task.

First, let's convert the signatures from [the Letter](https://docs.google.com/document/d/17ZqWl5grm_F5Kn_0OarY9Q2jlOnk200PvhM5e3isPvY/preview?pru=AAABc1PG4BU*eZAbZVBauzD5D9HRu-u9eQ){:target="_blank"} to something R can work with -- I just copied the table, removed the indices and replaced the tabs with semicolons. Rather than saving it as a CSV and importing it, in the interest of transparency, I pasted the data into the code so you can see it.

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

Here's those results in a bar graph. 

![Why are we doing this](/assets/pinker_letter.png){:style="height:600px;"}

Take from this what you will. Don't @ me.

I want to be crystal clear about one thing: even if the Letter was written *exclusively* by students, that shouldn't discredit their claims *a priori*. A lot of Pinker defenders criticize the Letter and its proponents as levelling *ad hominem* attacks against Pinker -- what is this, if not that? Pinker is using the identities of the Letter signatories as a tactic to invalidate its claims. Those claims should be addressed, rather than nitpicking or attacking an often arbitrary status. (Have you seen the academic job market??)

I'm going to stop there before I go off in a tangent. Again, this post is just to quantify *who* signed the letter, because some people think that matters.

I even hesitated to write this post for fear of giving credence to this kind of argument. But in the end, I wanted to show that, playing by these (harmful!) rules, dismissing the Letter based on the status of the people who signed it is not as easy as, ahem, *certain people* have made it out to be.

Post-script: Some people have already compiled a further breakdown of these numbers (e.g., tenure status). I hear that info should be public soon.
___
## The code
{% highlight r %}
sign = read.csv2(text = "
A, Pranav;Science Park, Hong Kong;NLP Engineer
Abner, Natasha;University of Michigan;Assistant Professor
Abramovitz, Rafael;MIT;PhD student
Ackerman, Lauren;Newcastle University;
Adamson, Luke;Harvard University;Postdoctoral Researcher
Adger, David;Queen Mary University of London;Professor of Linguistics
Ahmed, Anaïs;;
Ahmed, Samuel;;
Ahn, Byron;Princeton;Assistant Professor
Alam ,Marghoob;;
Alden, Paul;University of Maryland;
Altshuler, Daniel;University of Oxford;Associate Professor
Ananthanarayan, Sunkulp;The University of Texas at Austin;
Anderson, Carolyn;University of Massachusetts, Amherst;PhD candidate
Anderson, Catherine;McMaster University;Associate Professor
Andersson, Samuel;Yale University;PhD Student
Antonenko, Andrei;Stony Brook University;Lecturer
Aravind, Athulya;MIT Linguistics;Assistant Professor
Arehalli, Suhas;Johns Hopkins University;PhD student
Arnett, Catherine;UC San Diego;Graduate Student
Arregi, Karlos;The University of Chicago;Associate Professor
Arunachalam, Sudha;New York University;Associate Professor
Asinari, Sarah;University of Connecticut;PhD Student
Atkinson, Emily;University of Michigan;Postdoctoral Research Fellow
Auderset, Sandra;UC Santa Barbara;PhD Candidate
Auger, Julie;Université de Montréal;Associate Professor
Austen, Martha;The Ohio State University;PhD Candidate
Babaji, Charles;;Analytical Engineer
Babinski, Sarah;Yale University;PhD Candidate
Bai, Justin;CU Boulder;PhD student
Baier, Nico;University of British Columbia;Postdoc
Baird, Maggie;University of Massachusetts, Amherst;PhD Student
Bakos, Jon;Indiana State University;Assistant Professor
Bakst, Sarah;University of Wisconsin–Madison;Postdoctoral Researcher
Ballwahn, Isaac;New York University;
Banerjee, Neil;Massachusetts Institute of Technology;PhD candidate
Baratta, Amy;;
Barchas-Lichtenstein, Jena;Knology;Researcher
Barnes, Sonia;Marquette University;Associate Professor
Baron, Bertille;Georgetown University;PhD Candidate
Baron, Christopher;MIT;PhD Student
Barros, Matthew;Washington University in St. Louis;Lecturer
Barry, Daniel;The Graduate Center, CUNY;
Bartell, Stefan;University of Delaware;graduate student
Barzilai, Maya L.;Georgetown University;PhD Candidate
Basu, Sanjay;Life Member, AAAI / Life Member, ACM;NLP Services
Bauman, Carina;NYU;Alum
Beam de Azcona, Rosemary G.;Escuela Nacional de Antropología e Historia;Professor
Becker, Kara;Reed College;Associate Professor
Becker, Michael;UMass Amherst;
Beckman, Mary;;Fellow, Linguistics Society of America
Beer, Samuel;University of Virginia;Postdoctoral Researcher
Belew, Anna;University of Hawai'i at Mānoa;Adjunct Assistant Professor
Bell, Elise;UCLA;
Bell, Regina;Binghamton University;Alum
Bender, Emily M.;University of Washington, Department of Linguistics;Professor
Benkato, Adam;UC Berkeley;Assistant Professor
Bennett, Ryan;University of California, Santa Cruz;Associate Professor
Berez-Kroeker, Andrea;University of Hawai'i at Mānoa Department of Linguistics;Associate Professor
Berhow, Lori;Iowa State University;Alum
Bermúdez, Natalia;University of Chicago;Assistant Professor
Biers, Kelly;University of North Carolina at Asheville;Assistant Professor
Bigelow, Lauren;University of Toronto;PhD Student
Bisnath, Felicia;University of Michigan, Ann Arbor;PhD student
Bjorkman, Bronwyn;Queen’s University;Assistant Professor
Blamire, Emily;University of Toronto;
Blaxter, Tamsin;Gonville & Caius College, University of Cambridge;
Blix, Hagen;New York University;PhD Candidate
Blum, Eileen;Rutgers University;PhD Candidate
Blum, Mirella;University of Edinburgh;Student
Blümel, Andreas;University of Göttingen;Postdoctoral researcher
Bodeveryy, Lise;Vanderbilt University;Alum
Borer, Hagit;Queen Mary University of London;Department chair
Bossi, Madeline;UC Berkeley;
Bouavichith, Dominique A.;University of Michigan;PhD Candidate
Bourgerie Hunter, Marie;;Private sector computational linguist
Bowen, Caroline;Macquarie University;Research Fellow
Bowern, Claire;Yale university;Professor
Bowie, David;University of Alaska Anchorage;Professor
Bowman, Samuel R.;New York University;Assistant Professor
Bradley, Evan;Penn State University;Associate Professor of Psychology
Brickhouse, Christian;Stanford;PhD candidate
Brodkin, Dan;UC Santa Cruz;PhD Student
Brown, Meredith;;
Brunetto, Valentina;University of Leeds;
Buchwald, Adam;New York University;
Bui, Thuy;Hoa Sen University;Assistant Professor
Burkholder, Ross;Calvin University;Affiliate Professor
Butler, Becky;University of North Carolina at Chapel Hill;Adjunct Assistant Professor
Byrd, Andrew;University of Kentucky;Associate Professor of Linguistics
Cable, Seth;University of Massachusetts Amherst;Associate Professor
Callesano, Salvatore;University of Illinois at Urbana-Champaign;Assistant Professor
Campbell-Kibler, Kathryn;Ohio State University;
Campolong, Kelsey;Ulster University;PhD Researcher
Canjura, Julian;Northern Arizona University;Graduate student
Canning, Dominique;University of Michigan;PhD Candidate
Carmichael, Katie;Virginia Tech;associate professor
Carruthers, Brendan;Cognitive Science B.A.;
Carstens, Vicki;Southern Illinois University Carbondale;Professor & Chair
Catlin, Sara;Stony Brook University;
Chacón, Dustin A.;New York University Abu Dhabi;Research Scientist
Chadwick, Stacie;;
Chaiphet, Khanin;Stony Brook University;PhD Student
Chambers, Summer;University of Virginia;Linguistics MA
Chang, Charles B.;Boston University;Associate Professor
Chatten, Alicia;New York University;
Chemey, Natasha;Rutgers University;Graduate Fellow
Chen, Daniel;CU Boulder;PhD student
Chen, Tingchun;;
Cheng, Hung-Shao;New York University Department of Communicative Sciences and Disorders;PhD student
Chong, Adam;Queen Mary University of London;Lecturer
Christofori, Ulrike;San Joaquin Delta College;Instructor
Clare, Emily;;
Clark, McKenzie;;Student
Clark, Tallis;McGill University;Student
Clauss, Michael;University of Massachusetts Amherst;
Clem, Emily;University of California, San Diego;Assistant Professor
Clemens, Lauren;University at Albany;Assistant professor
Clevenger, Joanna;California State University, San Bernardino;Graduate Student
Clifford, Lily;Stanford University;PhD Student
Clopper, Cynthia;Ohio State University;Professor
Cockrum, Paul;The Ohio State University;Graduate Student
Collister, Lauren B.;University of Pittsburgh;Faculty Librarian
Conner, Katherine;The Ohio State University;PhD Student
Connor, Janet;University of Chicago;PhD Candidate
Conrod, Kirby;University of Washington;
Coon, Jessica;McGill University;Associate Professor
Coons, Caitlin;The University of Texas at Austin;PhD student
Copeland, Samantha;University of North Texas;Student
Cornall, Termy;;
Cotter, William;University of Arizona;
Cournane, Ailís;New York University;Assistant Professor
Cowper, Elizabeth;University of Toronto;
Cox, Julia;;
Cox, Taylor;Arizona State University;Research Technician
Craft, Justin T.;University of Michigan;Ph.D Student
Craioveanu, Radu;University of Toronto;PhD candidate
Crouch, Caroline;UC Santa Barbara;graduate student
Crowley, Archie;University of South Carolina;PhD Student
Culbertson, Jennifer;University of Edinburgh;Reader
Cunningham, Emma;;Software Engineer
D'Angelo, Jason;Georgetown University;Phd. Candidate
D’Arcy, Alexandra;University of Victoria;Professor
Dabkowski, Meghan;University of Delaware;Assistant Professor
Dahlberg-Dodd, Hannah;;
Daitya, Patrick;Monash University Linguistics Society;President
Daland, Robert;Apple, Inc.;Software Engineer
Dale, Christopher;;
Danis, Nicholas;Washington University in St. Louis;Lecturer
Davidson, Diana;;
Davidson, Lisa;NYU;Professor
Davis, Emory;Johns Hopkins University;Postdoctoral Fellow
Davis, Jenny;University of Illinois, Urbana-Champaign;Associate Professor
de Haas, Nynke;Utrecht University;Lecturer
De Santo, Aniello;University of Utah;Assistant Professor
de Vries, Hanna;Leiden University;Lecturer
Déchaine, Rose-Marie;University of British Columbia;Associate Professor
DeGiulio, Stephen;Santa Fe Community College;Professor
DeMarco, Stephanie;Birmingham City University;Education Developer
Denis, Derek;University of Toronto Mississauga;Assistant Professor
DeRoma, Cynthia Zocca;Yale University;Lector
Devlin, Kerri;UCLA;Graduate Student
Dewey-Findell, Martin;University of Nottingham;Assistant Professor
Dewey-Findell, Tonya Kim;University of Nottingham;Visiting Research Fellow
Dial, Heather;The University of Texas at Austin;Postdoctoral Fellow
DiCanio, Christian;University at Buffalo;Assistant Professor
Dinkin, Aaron;San Diego State University;Assistant Professor
Dockum, Rikker;Swarthmore College;Visiting Assistant Professor
Dolatian, Hossep;Stony Brook University;Alum
Doliana, Aaron;University of Maryland;PhD Student
dos Santos, Wesley;University of California, Berkeley;PhD student
Drackley, Patrick;University of Illinois at Urbana-Champaign;PhD Candidate
Drake, Shiloh;;
Driscoll, Trevor;MIT;
Drummond, Emily;University of California, Berkeley;Graduate student
Duncan, Daniel;Newcastle University;Lecturer in Sociolinguistics
Dupuy, Alexandra;Université du Québec à Montréal (UQAM);Graduate student
Durryyah, Nazahat;Boston University;Alum, Linguistics Blogger
Dusek, Ondrej;Charles University, Prague;Assistant Professor
Easterday, Shelece;University of Hawai'i at Mānoa;Assistant Professor
Eberhardt, Maeve;University of Vermont;Associate Professor
Elliott, Patrick;Massachusetts Institute of Technology;Postdoctoral Associate
Esipova, Maria;Princeton University, Program in Linguistics;Postdoctoral Research Associate
Everdell, Michael;The University of Texas, Austin;PhD Student
Farinella, Alessa;UMass Amherst;PhD Student
Farkas, Rebecca;;
Farris-Trimble, Ashely;Simon Fraser University;Associate Professor
Faytak, Matthew;UCLA;Postdoctoral Fellow
Feeny, Graham;New York University Department of Communicative Sciences and Disorders;PhD Student
Feldscher, Cara (Danny);Michigan State University;PhD graduate
Figueroa, Megan;University of Arizona;
Finley, Sara;Pacific Lutheran University;Associate Professor
Fleckenstein, Kristen;Coastal Carolina University;Assistant Professor
Fleisher, Nicholas;University of Wisconsin-Milwaukee;Associate Professor
Fletcher, Lauren;University of Edinburgh;PhD Student NLP
Fong, Suzana;MIT;graduate student
Forrest, Jon;University of Georgia;Assistant Professor
Fox, Bonnie;University of Hawai'i;
Francez, Itamar;University of Chicago;Associate Prof.
Francis, Elaine;Purdue University;Associate Professor
Franich, Kathryn;University of Delaware;Assistant Professor
Fraser, Katherine;University of the Basque Country;PhD Student
Freeman, Aaron;UPenn;Alum
Frishberg, Nancy;;
Fruehwald, Josef;University of Kentucky;Assistant Professor
Fuchs, Martin;Utrecht University;Postdoctoral Researcher
Gaby, Alice;Monash University;
Gadanidis, Tim;University of Toronto;PhD student
Gal, Susan;University of Chicago;professor
Ganeshan, Ashwini;Ohio University;Assistant Professor
García León, Javier;University of North Carolina at Charlotte;Assistant Professor
Gardner, Bethany;Vanderbilt University;PhD student
Garrett, Andrew;UC Berkeley;Professor & LSA Fellow
Garza, Joyhanna;UCSB Linguistics;PhD Candidate
Gasser, Emily;Swarthmore College;Assistant Professor
Gautam, Vasundhara;Dialpad;Speech Recognition Engineer
Gebhard, Jessica;;
Gegg-Harrison, Whitney;University of Rochester;Associate Professor
Geguera, Ria Mai;NYU;Research Staff
Geissler, Christopher;Yale University;PhD Candidate
Gerald, JPB;CUNY - Hunter College;
German, Austin;The University of Texas at Austin;PhD student
Getz, Heidi;;
Getzen, Cara;;TESL Student
Gillon, Carrie;The Vocal Fries;Co-host
Glödstaf, Walther;University of Illinois Urbana Champaign;PhD student
Goad, Heather;McGill University;Associate Professor
Göbel, Alexander;University of Massachusetts, Amherst;Graduate Student
Gölz, Miriam;Brandeis University;graduate student
Gonering, Brennan;UC Davis;Graduate student
Gonzalez-Marquez, Monica;RWTH;
Good, Jeff;University at Buffalo;Professor
Gorman, Kyle;Graduate Center, City University of New York;
Govindarajan, Venkata S;University of Texas at Austin;PhD Student Computational Linguistics
Gowda, Yadav;MIT;PhD student
Grama, James;University of Duisburg-Essen;Research Fellow
Green, Caitlin;;
Green, Elizabeth;University of Texas at Austin;
Greenbank, Emily;Victoria University of Wellington;Research Fellow
Greenwood, Anna;Google;Program Manager
Greeson, Daniel;Michigan State University;Graduate student
Grestenberger, Laura;University of Vienna;Assistant Professor
Grieve-Smith, Angus;The New School;
Grishin, Peter;MIT;PhD Student
Grothues, Natalie;University of Colorado Boulder;PhD student
Guo, Alice;University of Toronto;Alum
Haber, Eli;University of Chicago;
Hagedorn, Christina;City University of New York - College of Staten Island;Assistant Professor
Hagiwara, Robert;University of Manitoba;
Hall-Lew, Lauren;University of Edinburgh;Reader
Hall, Daniel Currie;Saint Mary's University, Halifax, Nova Scotia;associate professor; LSA member
Halpert, Claire;University of Minnesota;Associate Professor
Hansen, Daniel;University of Chicago;PhD Student
Hao, Yiding;Yale University;PhD Candidate
Harley, Heidi;University of Arizona;Professor
Harper, Sarah;University of Southern California;PhD Candidate
Harvey, Meg;University of Arizona;
Haslinger, Nina;University of Göttingen;PhD Candidate
Hauk, Bryn;;
Heap, David;University of Western Ontario;Associate Professor
Heath, Jevon;University of Pittsburgh;Director of Undergraduate Studies
Heaton, Hayley;University of Michigan;Linguistics PhD
Heider, Paul;Medical University of South Carolina;Senior Research Scientist
Henderson, Robert;University of Arizona;Associate Professor of Linguistics
Hendery, Rachel;Western Sydney University, Australia;Associate Professor
Henley, Katherine;;
Henry, Cassidy;University of Maryland;
Hetherington, Rebecca;University of Melbourne;
Hill, Angelica;University of Massachusetts Amherst;PhD student
Hogan, Caitlin;Queen Mary University of London;Graduate Student
Holgate, Eric;University of Texas at Austin;PhD. Candidate
Holladay, Kaden;University of Massachusetts Amherst;PhD Student
Hoops, Tracie;CSU Fullerton;MA student
Hope, Maxwell;University of Delaware;PhD student
Horesh, Uri;Achva Academic College;
Hou, Lynn;University of California, Santa Barbara;
Hughes, Brianne;;MA Linguistics
Hyett, James;University of Toronto;Alum
Irvine, Melissa;;
Jacobs, Cassandra;University of Wisconsin;Postdoctoral Researcher
Jaggers, Zachary;University of Oregon;Postdoctoral Scholar
Jamieson, E;University of Edinburgh;
Janoff, Arianna;;
Jenks, Peter;UC Berkeley;Associate Professor
Jensen, Monica;University of Washington;PhD Student
Jent, Brandon;University of Kentucky;Alumnus, MA Linguistic Theory and Typology
Jeong, Sunwoo;Seoul National University;Assistant professor
Jeretic, Paloma;New York University;PhD Candidate
Jerro, Kyle;University of Essex;Lecturer
Jones, Kyra;;
Jones, Taylor;University of Pennsylvania;PhD Graduate
Joyce, Taylor;The University of Texas at Austin;PhD Student
Kalin, Laura;Princeton University;Assistant Professor
Kane, Aurora;University of California, Berkeley;PhD Student
Karlin, Robin;UW-Madison;Postdoctoral researcher
Kasstan, Jonathan;University of Westminster;Assistant Professor
Kastner, Itamar;University of Edinburgh;
Kennedy, Robert;University of California, Santa Barbara;Senior Lecturer
Khan, Sameer ud Dowla;Reed College;Associate Professor
Kiesling, Scott F.;University of Pittsburgh;Professor & Chair
Kim, Christina;University of Kent;Senior lecturer
Kim, Judy;Yale University;Postdoc
Kimper, Wendell;University of Manchester;Lecturer
Kirchner, Jessica;Google;Senior Linguist
Klassen, Jeffrey;University of Saskatchewan;Sessional Lecturer
Klausner, Lukas Daniel;St. Pölten University of Applied Sciences;Researcher
Klecha, Peet;;Linguist
Koesterich, Niki;Tel Aviv University;Graduate Student
Kolozsvari, Robyn;;
Konnelly, Lex;University of Toronto;PhD Candidate
Kosse, Maureen;CU Boulder;Grad Student
Kostyszyn, Kalina;Stony Brook University;PhD student
Kotek, Hadas;;Computational Linguist
Koulidobrova, Helen;Central Connecticut State University;Associate Professor
Koval, Pasha;University of Connecticut;PhD candidate
Kramer, Ruth;Georgetown University;
Kraus, Kaj;Gallaudet University;PhD Student
Kraus, Kelsey;UC Santa Cruz;PhD graduate
Kucharska, Rosa;University of Manchester;Undergraduate student
Kuo, Annita;;
Kush, Dave;NTNU;Associate Professor
Lai, Catherine;University of Edinburgh;
Lalonde, Codie;Carleton University;PhD Candidate
Lang, Benjamin;New York University Abu Dhabi;
Laparle, Schuyler;UC Berkeley;PhD Candidate
Laperle, Samuel;;
Lassahn-Worrell, Price;;
Laturnus, Rebecca;;
Lau-Preechathammarach, Raksit;UC Berkeley;Graduate Student
Laurentine, Kyle;;
Lawson, Alexandra;University at Buffalo, SUNY;Graduate Student
Le Mené, Marine;University of Strasbourg;Postdoctoral Researcher
Leach, Hannah;University of Newcastle;Lecturer
Lee-Goldman, Russell;Google;
Lee, Naomi;New York University;PhD student
Lee, Rebecca;University of Colorado Boulder;PhD student
Lee, Si Kai;UConn;PhD Student
Leonard, Wesley;University of California, Riverside;Associate Professor
Lesho, Marivic;;
Lesk, Katharina;University of Vienna;student
Levi, Susannah;NYU;
Levinson, Lisa;University of Michigan;Lecturer
Lewis, Rebecca;University of Connecticut;PhD Student
Lewis, Tom;Georgia Southern University;Visiting Instructor
Li, Neh Gnetnemt;Jinggangshan University;Research Scientist
Li, Noriyasu;;
Lilley, Kevin;The Ohio State University;PhD Student
Lindsey, Kate;Boston University;
Liter, Adam;University of Maryland;Graduate student
Litovsky, Celia;Johns Hopkins University;PhD candidate
Little, Alexa;7000 Languages;Executive Director
Loos, Cornelia;University of Hamburg;Postdoc
Love-Nichols, Jessica;Macalester College;Visiting Assistant Professor
Lowry, Cass;The Graduate Center, City University of New York;PhD student
Lu, Deedee;;
Lu, Jiayi;Stanford University;PhD student
Lucek, Stephen;University College Dublin;Postdoctoral Fellow
Lukyanenko, Cynthia;George Mason University;Term Assistant Professor
Lund, Gunnar;Harvard;PhD candidate
Lyskawa, Paulina;University of Maryland;PhD student
MacGregor, Caiden;La Trobe University;Graduate student
MacKenzie, Jordan;Georgetown University;PhD Candidate
MacKenzie, Laurel;New York University;Assistant Professor
Macknick, Anna;Princeton University;Undergraduate student
Mahan, Heather;UCSC;MA Linguistics graduate
Maier, Erik Hans;UC Berkeley;PhD Candidate
Mailhot, Frederic;Dialpad, Inc.;Computational Linguist
Malamud, Sophia A.;Brandeis University;Associate Professor
Maldonado, Mora;University of Edinburgh;Postdoctoral researcher
Manetta, Emily;University of Vermont;Professor and Chair, Department of Anthropology
Manfredi, Victor;Boston University;Visiting Researcher
Mangold, Ina Runa;University of Edinburgh;Postgraduate Student
Manke, Christine;California State University, Northridge;Alumna
Manning, Emma;Georgetown University;PhD Student
Mansfield, Courtney;University of Washington;PhD Candidate
Mantenuto, Iara;University of California, Los Angeles;PhD Candidate
Marino, D.;McGill University;Grad Student
Martí, Luisa;Queen Mary University of London;Senior Lecturer
Martin, Fabienne;Humboldt-Universität zu Berlin;
Martin, Katie;MIT;Graduate student
Martin, Tyree;University of Arizona;Ph.D. Student
Martinez del Rio, Aurora;University of Chicago;Graduate Student
Martinez, Randi;Yale University;
Matsubara, Julie;University of Chicago, English Language Institute;Director
Mauk, Claude;University of Pittsburgh;Senior Lecturer
McBride, Justin T.;Northeastern State University;Assistant Professor
McCabe, Samantha;;
McClay, E. K.;Simon Fraser University;research staff
McCoy, Tom;Johns Hopkins University;Graduate student
McCready, Elin;Aoyama Gakuin University;Professor
McFadden, Thomas;Leibniz-Zentrum Allgemeine Sprachwissenschaft;
McGowan, Kevin;University of Kentucky;Assistant Professor
McKay, Isabel;University of Arizona;
McPherson, Laura;Dartmouth College;Associate Professor
McVeigh, Joe;University of Jyväskylä;University teacher
Meadows, Tom;Queen Mary University of London;PhD Candidate
Medina, Jennifer;;
Merryweather, Marina;;
Mesh, Kate;Lund University;Postdoctoral Researcher
Meyer, Cherry;University of Michigan;
Michael Gasser;Indiana University;Associate Professor Emeritus
Midgley, Daniel;Because Language;Co-presenter
Mieczkowski, Hannah;Stanford University;PhD candidate, Communication
Miller, Taylor;SUNY Oswego;Visiting Assistant Professor
Minnick, Lisa C.;Western Michigan University;Associate Professor
Mirea, Nicole;Northwestern University;PhD student
Molina, Malia;Carleton College;
Monette, James;;Data Scientist
Mooney, Kate;New York University;
Moraski, Kendall;University of British Columbia;Alum
Morgan, Adam;NYU;Postdoc
Morikawa, Nora;;
Mufwene, Salikoko S.;University of Chicago;Professor of Linguistics
Munson, Benjamin;University of Minnesota;Professor and Chair
Murphy, AJ;University of South Carolina;PhD Student
Murray, Sarah;Cornell University;Associate Professor
Musica, Anne;Georgetown University;Alum
Musil, Jakub;The University of Edinburgh;PhD candidate
Nadathur, Prerna;Heinrich Heine University;Postdoctoral researcher
Nakamura, Megan;University of Florida;
Namboodiripad, Savithry;University of Michigan;Assistant Professor
Narayan, Chandan;York University Linguistics;Assoc Professor
Nault, Charlène;Université du Québec à Montréal (UQAM);MA student
Nederveen, Sander;Simon Fraser University/University of British Columbia;MA/PhD student
Nelson, Brett;University of Calgary;PhD Candidate
Nelson, Scott;Stony Brook University;
Nesbitt, Monica;Dartmouth College;Postdoctoral Researcher
Newell, Heather;UQAM;Professor
Ng, Sara;University of Washington;PhD student
Nguyen, Chieu;Google Japan;Computational Linguist
Nguyen, Emma;University of Connecticut;PhD student
Niedzielski, Nancy;Rice University;Associate Professor
Nielsen, Kuniko;Oakland University;Associate Professor
Nölle, Jonas;University of Edinburgh;PhD Candidate
Noonan, Máire;Université de Montréal & Université du Québec à Montréal,;course lecturer
Norris, Mark;;
Nowlan, Melody;;
Nycz, Jennifer;Georgetown University;Associate Professor
O'Gorman, Tim;University of Massachusetts Amherst;Postdoctoral Researcher
O'Hara, Charlie;University of Southern California;
O'Meara, Carolyn;Universidad Nacional Autónoma de México;Associate Research Professor
O'Neill, Brittney;York University;PhD student
Orfitelli, Robyn;University of Sheffield;Lecturer
Ostrove, Jason;UC Santa Cruz;Lecturer
Overfelt, Carly;;
Pabst, Katharina;University of Toronto;Ph.D. Candidate
Palma, Pauline;McGill University;PhD student
Papillon, Maxime;University of Maryand;
Parrish, Alicia;New York University;Grad student
Parrott, Jeffrey Keith;Department of English and American Studies, Palacký University in Olomouc;Assistant Professor of Linguistics
Pasquinelli, Renni;Johns Hopkins University;PhD Student
Pasternak, Robert;Leibniz-Center for General Linguistics;Postdoctoral Researcher
Pater, Joe;University of Massachusetts Amherst;Professor
Patton, Colleen;University of Arizona;PhD Candidate
Paul, Ileana;University of Western Ontario;Associate Professor
Paullada, Amandalynne;University of Washington;PhD Candidate, Linguistics
Payne, Amanda;;
Payne, Elena;University of Cambridge;Student
Payne, Elinor;University of Oxford;Associate Professor
Pearce, Jo;University of Glasgow;PhD Student
Pearson, Hazel;Queen Mary University of London;Senior Lecturer
Perez Borbon, Luz;University of Massachusetts Boston;PhD student
Perfors, Amy;University of Melbourne;Associate Professor
Perleberg, Ellen;University of Washington;Undergraduate
Peters, Andrew;University of Toronto;PhD Candidate
Pham, Mike;;
Piggott, Glyne;McGill University;Emeritus Professor
Pillion, Betsy;University of Chicago;PhD Candidate
Pinzin, Francesco;Goethe Universität Frankfurt;Postdoctoral researcher
Plumb, May Helena;University of Texas at Austin;PhD Candidate
Pollio-Barbee, Harper;Brandeis University;Undergraduate Student
Potter, David;Morehead State University;Post-doc
Potvin, Gabrielle;;
Pratt, Teresa;San Francisco State University;Assistant Professor
Preminger, Omer;University of Maryland;Associate Professor
Prichard, Hilary;;Linguistics PhD
Prickett, Brandon;;
Puderbaugh, Rebekka;University of Edinburgh;Teaching Fellow
Punske, Jeffrey;Southern Illinois University Carbondale;Associate Professor & Director of Undergraduate Studies
Purse, Ruaridh;University of Pennsylvania;PhD Candidate
Raclaw, Joshua;West Chester University;Assistant Professor
Rademacher, Tess;Former LSA Intern;
Rasin, Ezer;Leipzig University;Postdoctoral Researcher
Rawlins, Kyle;Johns Hopkins University;Associate Professor
Reed, Paul E.;University of Alabama;Assistant professor
Rees, Alice;University of Edinburgh;Research Fellow
Rehrig, G.;UC Davis;Postdoctoral Researcher
Reiss, Charles;Concordia University, Montreal;Professor
Remirez, Emily;UC Berkeley;PhD Candidate
Rett, Jessica;UCLA;Professor and Director of Graduate Studies
Richardson-Todd, Aurore;;PhD student
Richie, Russell;University of Pennsylvania;Postdoctoral Fellow
Ritch, Joseph;University of Hawai'i at Mānoa;MA Student
Rivard, Alex;Carleton University;
Roberts, Brice;University of California, Los Angeles;PhD Candidate
Roberts, Julie;University of Vermont;Professor and Director
Robinson, Mary;NYU;PhD student
Robles, Jessica S.;Loughborough University;Lecturer
Rodriguez, Alejandro;UC San Diego;PhD Student
Rodriguez, Jamilläh;University at Albany, SUNY;Ph.D. student
Ronkos, Danielle;The Graduate Center, CUNY;Ph.D. Candidate
Rosa, Jonathan;Stanford University;Associate Professor
Rosen, Nicole;University of Manitoba;Professor
Rosenau, Sara;CU Boulder;Graduate Student
Rouvier, Ruth;University of California, Berkeley;PhD Candidate
Rouvinen, Alina;;Student
Rowe, Margaret Anne;Georgetown University;Alum
Royer, Adam;UCLA Linguistics;PhD Candidate
Royer, Justin;McGill University;PhD Student
Sampson, Tory;University of California, San Diego;PhD Student
Sanchez, Roger;Universidade Federal de Belo Horizonte, Brazil;PhD
Sandoval, Starr;;graduate student
Sandy, Abu El Adas;NYU;PhD student/worker
Sarver, Isaac;Michigan State University;Graduate Student
Sayeed, Asad;University of Gothenburg;Assistant Professor
Scarpace, Daniel;University of Texas at Arlington;Assistant Professor of Instruction
Schaefer, Florian;Humboldt Universität zu Berlin;Lecturer
Scheffler, Tatjana;University of Potsdam;Postdoctoral Researcher
Schlegl, Lisa;Univeristy of Toronto;PhD Student
Schneider-Zioga, Patricia;California State University, Fullerton;Associate Professor
Schneier, Joel;University of Central Florida;Lecturer
Schwartz, Richard G.;CUNY Graduate Center;Presidential Professor
Seals, Corinne;Victoria University of Wellington;Senior Lecturer
Sears, Cheyenne;Ohio University;Alum
Semushina, Nina;UCSD;PhD candidate
Seong, Jihye;The State University of New York at Buffalo;Ph.D. Student
Shames, Kayla Matthea;Cornell University;Undergraduate Student
Shan, Chung-chieh;Indiana University;Associate Professor
Shapiro, Mary;Truman State University;Professor of Linguistics
Sheen, Jisu;Yale University;Postbaccalaureate researcher
Shenkar, Julia;George Mason University;Alum
Sherley-Appel, Clara;UCSC, UVA;Linguistics MA
Showers-Curtis, Katka;University of Wisconsin - Madison;Graduate Student
Shukla, Mohinish;;
Shulist, Sarah;Queen’s University;Associate Professor
Sichel, Ivy;UC Santa Cruz;Associate Professor
Sicoli, Mark A;University of Virginia;Assistant Professor
Simpson, Erin;UCL Institute of Education;PhD student
Sims, Nandi;Ohio State University;PhD Candidate
Singerman, Adam;Department of Linguistics, University of Chicago;Postdoctoral Teaching Fellow
Sirna, Sarah;Michigan State University;
Skilton, Amalia;University of Texas at Austin;Postdoctoral Researcher
Slayton, Aliya;University of Hawai'i at Mānoa;PhD student
Slobe, Tyanna;University of California Los Angeles;PhD Candidate
Smith, Alexander D.;University of North Texas;
Smith, Barry;University at Buffalo;Professor & Chair
Smith, James;;
Smith, Kaylin;Michigan State University;PhD candidate
Sneller, Betsy;Michigan State University;Assistant Professor
Snider, Todd;;Postdoctoral Research Fellow
Soldaini, Luca;Amazon;Applied Scientist
Sommerlot, Carly J.;University of Texas at Arlington;Ph.D. Candidate
Sonnenschein, Aaron Huey;California State University Los Angeles.;Professor
Sprenger, Anna-Marie;UChicago;graduate student
Staicov, Adina;Hiroshima University;Assistant Professor
Stalley, Sean;;
Stephens, Heather;University of Toronto;PhD Candidate
Stickles, Elise;University of British Columbia;Assistant Professor
Stromdahl, Lars;University of Delaware;PhD Student
Strother-Garcia, Kristina;Bloomsburg University;Assistant Professor
Subtirelu, Nicholas;Georgetown University;Assistant Professor
Sullivant, Ryan;University of Texas at Austin;
Sundaresan, Sandhya;;
Sunil Arvindam, Vishal;;
Surbatovich, Amy;;Editor
Sutherland, Paul;American Philosophical Society;Archivist, Linguist
Szabó, Ildikó Emese;New York University;PhD candidate
Tabachnick, Guy;New York University;graduate student
Tallman, Adam;CNRS;Postdoctoral researcher
Talmina, Natalia;Johns Hopkins University;PhD student
Taniguchi, Ai;University of Toronto Mississauga;Assistant Professor
Taylor, Katherine;The Ohio State University;Alum
Thomas, Airica;Northwestern University;PhD Student
Thomas, Jenelle;University of Oxford;
Thomas, William;The Ohio State University;PhD Student
Thompson, Anie;H5/University of California Santa Cruz;Consulting Linguist and PhD alum
Thompson, Ellen;Florida International University;Professor
Thompson, Katrina;University of Wisconsin-Madison;Professor
Thoms, Gary;New York University;Assistant Professor
Thornes, Tim;Boise State University;Associate Professor
Tomlin, Nicholas;UC Berkeley;PhD Student
Torbert, Benjamin;University of Missouri-St Louis;Associate professor
Torgersen, Henrik;University of Oslo;MA student
Tran, Marcellin;University of Toronto;Student
Travis, Lisa;McGill University;Professor Emeritus
Tulsyan, Purnima;;
Turnbull, Rory;Newcastle University;Lecturer
Turner, Gerry;York University;PhD Candidate
Turner, Robin;University of Illinois at Urbana-Champaign;PhD student
Twiner, Nicholas;Stanford University;Graduate Student
Tyler, Matthew;Yale University;PhD candidate
Tyrone, Martha;Long Island University;Associate Professor
Ulfsbjorninn, Shanti;University of Deusto, Bilbao.;Associate Professor
Umbal, Pocholo;University of Toronto;PhD Candidate
Usta, Betül Seda;University of Stirling;PhD student
Valentinsson, Mary-Caitlyn;Appalachian State University;Visiting Assistant Professor
van den Akker, M.;Radboud University Nijmegen, The Netherlands;Undergraduate
VanderStouwe, Chris;Boise State University;Lecturer
Vaughan, Alfie;University of Cambridge;Undergraduate
Vihman, Marilyn;University of York;Professor
Vihman, Virve;University of Tartu;Associate Professor
Villanueva, Mercedes Eileen;;
Vittalbabu, Chandru;Sunnyvale School District;Speech-Language Pathologist and Linguistics graduate
Vu, Mai Ha;University of Delaware;Alum
Walkden, George;University of Konstanz;Professor of Linguistics
Warner, Natasha;University of Arizona;Professor and Head
Warren, Isaac;Georgetown University;MS Student
Wassink, Alicia;University of Washington;
Weinberg, Miranda;Swarthmore College;Visiting Assistant Professor, Linguistics
Weirick, Josh;Purdue University;PhD student
Wells, Alexus;Georgetown University;
Whitcomb, Kathleen;;
Williams, Adina;;Research Scientist
Wilson, Brianna;University of Chicago;PhD Student
Wilson, Fiona;University of Toronto;Graduate Student
Wilson, Scott Keohookalani;Pukyong National University;Lecturer
Wing, Dakota;York University;PhD Candidate
Wingett, Hannah;Georgetown University;Alum, BA Linguistics + MS Theoretical Linguistics
Winterstein, Grégoire;UQAM;Professor
Wöhrmann, Frithjof;University of Georgia;PhD Student
Wolf, Simon;Unaffiliated;Independent Researcher and Consultant
Wood, Skye;Virginia Tech;Alum
Wright, Kelly Elizabeth;University of Michigan;PhD Candidate
Yeaton, Jeremy;UC Irvine;PhD student in Language Science
Yoshida Nuttall, Kelly;Boise State University;
Young, Eris;;Writer
Yuan, Michelle;University of California, San Diego;Assistant Professor
Zaitsu, Anissa;Stanford University;PhD student
Zimman, Lal;UC Santa Barbara;Associate Professor of Linguistics
Zompi, Stanislao;;
Zweig, Eytan;University of York;Lecturer
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