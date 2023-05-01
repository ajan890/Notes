## Engineering Ethics in the Automobile Industry


### Case Study: Ford Pinto

Towards the end of the 1960’s, Ford Motor Company was losing market share to European car brands, which were producing smaller and cheaper cars.  Ford decided that they had to design a new car that was smaller and cheaper in order to compete with them.

In 1970, they released the Ford Pinto, which could sell on the market for less than $2000.  However, because of the rushed design, they did not priortize safety standards - as long as it could be approved by the government.  Their design placed the fuel tank directly below the back bumper of the car.

In 1978, three teenagers were in a Ford Pinto on the highway when they were rear-ended by a truck.  The fuel tank was damaged, resulting in an explosing that killed all three teens.  Elkart County then sued Ford for criminal homicide


#### Ford Memo



* Earlier, in 1977, the _Mother Jones_ magazine reported an “expose” that supposedly showed callous behavior on Ford’s part in designing and manufacturing the Pinto.  The Memo was presented as a “smoking gun” regarding Ford’s lack of ethics.  While there were ethical issues with the Pinto, they are not reflected in the memo.
* The memo was prepared by Ford on invitation by the National Highway Transportation Safety Administration, which wanted to develop risk-benefit and risk-cost-benefit analyses in their decision-making process.
* The memo was not “Secret”.  It was submitted to the NHTSA as part of the rule-making procedure for greater safety in automobile fuel safety systems.  Rather than “Secret,” the original is buried in a government archive somewhere in the Washington, D.C. area.
* The memo was intended solely to influence NHTSA’s regulation development
* The memo was NOT intended for any use within the Ford Motor Company
* The memo was never intended for distribution within Ford, either to design engineers or vehicle-recall staff
* The memo unknown to Ford design or safety engineers until after the publication of the _Mother Jones_ article
* The risk-cost-benefit analysis concerned rollovers, not rear end collisions.
* Since the design of the Pinto was done 1967-70, the memo could not have affected design and development
* Did not specifically mention the Pinto; it was an analysis of the risks and costs of proposed fuel safety requirements
* Was about ALL 11,000,000 cars sold in the United States, not specifically the Pinto
* Ford did not establish the $200,000 per life metric; it was value supplied by NHTSA, and was common throughout the government at that time.

![image](https://user-images.githubusercontent.com/66571533/235384882-937c0505-b80a-437d-b910-436e2c1186a5.png)


#### Was the Pinto a “Deathtrap?”



* Was it a death trap or simply a poorly designed subcompact?
* Based on the number of fatalities caused by the Ford Pinto compared to that of other cars, the Pinto is in the middle. Not the best, but also not the worst.


#### Are there Ethical Issues with the Pinto?



* Yes.  The most significant ethical issue with the Pinto was its fighting upgraded fuel safety standards.  Rather than try and examine problems with the Pinto (and related Ford products), it fought all the way until a recall was announced.  The fix was to strengthen the fuel filler tube and install a $3 plastic cap over the differential.  The total cost of the upgrade was $11 per car.
* The plastic cap had been required in Canadian models of the Pinto since Day 1.
* There were a total of 27 burn deaths from the Pinto.


### Case Study: Ford Explorer



* The Ford Explorer is an SUV, and they were advertising it for its power and size.
* However, with the way it was designed, its center of gravity is high up, making the car prone to rollovers.
* This is another Engineers vs. Management case:
    * Engineers recommended:
1. Lower the engine and CG (rejected)
2. Widen the Track (rejected)
3. Use smaller tires (rejected)
4. Stiffen the springs (done partially)
5. Lower tire pressure (done)
6. Degrade performance (rejected!)
* The car had a static stability factor of 1.07, which following the SSF graph predicts an approximately 0.37 chance of a rollover in a single vehicle incident.


### Case Study: GM Ignition Switch



![image](https://user-images.githubusercontent.com/66571533/235384814-d231e324-9d05-4f96-9670-16881fb813d1.png)




* A Detent Plunger is present in the shaft behind where the key is inserted to keep it in the off, accessory, or run positions.
* Since 2003, GM had a faulty detent plunger, which may cause the engine to shut off while the car was still rolling, preventing airbags from inflating.
* GM knew about the issue but did not do anything about it since it was expensive to fix.
* It was not until 2014, a court ruling fined GM $35 million, and forced them to recall and fix 2.6 million vehicles.  It was only until then that GM admitted they were at fault.


### Case Study: Volkswagen Defeat Device



* Volkswagen invented a defeat used to cheat on emissions tests.
    * It automatically detected when the car was being tested for emissions, and it tuned down the car’s performance and also turned on other equipment that helps reduce emissions.
    * When the car was not being tested, the defeat device was turned off, and the car’s emissions were considerably higher than legal limits.
    * This was done to keep the performance of the car while passing all of the tests.
* Affected Volkswagen and related products:
    * 2009-2015 2009-2015 Volkswagen Jetta
    * 2009-2015 Volkswagen Golf
    * 2010-2015 Audi A3
    * 2012-2015 Volkswagen Beetle
    * 2012-2015 Volkswagen Passat
    * 2009-2016 Porsche Cayenne Diesel
    * 2014-2016 Audi A6
    * 2014-2016 Audi A7
    * 2014-2016 Audi A8/A8L
    * 2014-2016 Audi Q5


## Biomedical Engineering Ethics



* The ethical principles of ethical practice in biomedical engineering are unique in that one is not only bound by the ethical precepts of the engineering profession, but also by medical ethics and the regulatory structures of the medical field - most notably the Food and Drug Administration (FDA) here in the United States.


### Case Study: Therac-25



* The Therac-25 was the third in a line of dual-use radiation therapy machines - machines that could irradiate a patient with either a low-energy electron beam or high-energy x-rays
* The Therac-6 and Therac-20 had hardware locks that requires an X-ray target to be in place before the high-energy x-ray mode can be used.  If the X-ray target was not present, the machine would not work.  However, in the Therac-25, the company switched all the hardware locks to software locks, and its central computer checked everything.  
* Because of this, there were six overdose events from 1985 to 1987, where four patients were killed and two were chronically injured by high amounts of radiation.
* The machine was recalled in 1987 because of these events.


#### Problems with Development



* Simple programming errors
* Inadequate safety engnieering
* Inadequate testing of software
* Poor computer-user interface design and testing
* Lax safety culture in design and manufacturing
* Inadequate response to reports of problems
* Inadequate reporting to FDA


#### Safety Analysis and Failure Mode and Effects Analysis



* No demonstrable basis for probabilities:
    * “Generic failure rate of software”: 10<sup>-4</sup> per hour
    * “Computer selects wrong mode”: 4 x 10<sup>-9</sup> 
    * “Computer selects wrong energy”: 10<sup>-11</sup> 
* The 8-second delay
    * When the operator began entering the specifics of a treatment protocol and the “Change Mode” choice was selected, an 8-second delay occurred when the bending magnets were resetting; during this time period, no additional data would be accepted by the computer - the specifics would default to the **_previous_** settings.
    * So, if the new setting was an electron beam (low power) treatment, the 8-second delay would revert to the previous setting - x-rays - and leave the collimator out of the beam, thus exposing the patient to a 25Mev electron beam


### Case Study: Bjork-Shiley Heart Valve



* The Bjork-Shiley Heart valve was constructed in two pieces: the rim and the inlet strut, and then the outlet strut was welded onto the rim.  Sometimes the weld was bad, but was sent out anyway.  Multiple deaths.


## Endovascular Technologies


### Aortic Stent



* An aortic aneurysm is a ballooning of the aorta as it descends from the heart.  It is usually fatal if left untreated.  Major surgery was one option, but Endovasular Technologies of Menlo Park had a better idea: a stent.
    * Essentially a metal skeleton inside a fabric graft.
    * The graft works by exerting pressure above and below the aneurysm to limit circulation
    * This works the vast majority of time, but can possibly lead to death of the aneurysm ruptures


### Guidant Prizm Defibrillator



* Essentially a pacemaker
* In March, 2005, a college student with a Guidant Prizm Defibrillator died during a bike ride when the pacemaker short-circuited and was fried.
* Engineers of Guidant found an error with manufacturing the defibrillators and fixed them in the newer iterations.  However, they kept the hardware failure a secret from patients and physicians.
* They continued selling defibrillators they produced before the chance and also lied about the chance of failure.
* Guidant - Endovascular Technologies Finances
    * **Costs to EVT/Guidant**
        * EVT Criminal Fines - $93.5 million
        * EVT Civil Settlements - unknown
        * Guidant Prizm Criminal Fine - $293.5 million 
            * (false reporting to FDA)
        * Guidant Prism Civil Fine - $9.2 million
            * (false claims to Medicare)
        * Guidant Civil Settlements - est. $200 million


### Olympus Duodenoscope



* The Olympus Duodenoscope was developed as an insertable clinical instrument that could help with diagnosis and treatment in a variety of thoracic organs (ex. gall bladder)
* Unfortunately, when cleaned and washed between patients, not all infectious particles could be removed from the small crevices in the head of the device.
* This resulted in 35 deaths and over 350 infections, usually involving hospitalization.


### Synthes Bone Cement



* Synthes was an old Swiss company best known for its bone stabilization pins and screws
* About 2000, it began to develop and market a bone cement that could be injected into the spinal column of osteoporosis patients.
* However, they began doing this without being approved by the FDA and without warning patients about the possible risks, even though some of their laboratory tests concluded that it may kill some patients.


### Cutter Polio Vaccine



* You could live with heavy steel braces on your legs…
    * Like President Roosevelt
* or live in an iron lung
* In 1910-1955, polio incidence grew, slowly, then exponentially after World War II.


#### Quotes



* “Or so it appeared. During the 1954 trials, each lot of polio vaccine had been triple-tested for safety—by the NIH, by Salk’s laboratory, and by the companies themselves. But then, in the rush following the release of the Francis report, this system came apart. The NIH did very little testing, and the results it got are still shrouded in mystery. One of its top researchers claimed, years later, that safety problems surrounding lots of newly licensed polio vaccine were consciously ignored. “We had eighteen monkeys,” said Dr. Bernice Eddy, and NIH staff microbiologist. “We inoculated [them] with each vaccine that came in. And we started getting paralyzed monkeys.”
* The infected lots belonged to Cutter, Eddy recalled. She reported these findings to her superiors, along with photos of the monkeys, but nothing was done. “They just went ahead and released the vaccine anyway, a lot of it,” she said. “The monkeys, they just discarded.” [Oshinsky, p. 231]
* Julius Youngner, for example, told of accepting an invitation to visit the Cutter vaccine factory in the days following the Ann Arbor announcement [this could only have been Wednesday, April 13, Thursday, April 14, or Friday, April 15, 1955]. ‘I was appalled,’ he said. ‘Tanks containing live-virus pools and other tanks containing virus lots in various lots in various stages of formalin inactivation were kept in the same rooms. Conditions were not neat or esthetically appealing. There was a worrisome lack of attention to the most basic rules… They never let me look at their data, but it was obvious to me that they were having serious trouble with their inactivation procedures.”
* “My plan,” he noted, “was to return to Pittsburgh and immediately warn the powers-that-be to hold off licensing Cutter or, if this was not possible, to stop distribution temporarily of their vaccine. I was frightened to think of the sloppiness of their operation.” According to Youngner, he went to see Salk, told him “that the people at Cutter didn’t know what they were doing,” and said he was going to write a letter “detailing my impressions” to both Basil O’Connor [director of the National Foundation for Infantile Paralysis] and the NIH. “Jonas,” he recalled, “was unexpectedly calm through my recital. He agreed that it was a serious situation with terrible potential consequences. For this reason he suggested that it would be better if the letter came from him…  I was completely taken in—to my knowledge the letter was never written. Jonas never gave me a copy of it, and he never mentioned the matter to me again… 
* When the Cutter incident began to unfold. . . . I was immobilized. I realized that Jonas probably had done nothing –but neither had I. My guilt at being taken in by him was oppressive, but what to do? Silence was my response.”


#### Aftermath



* Although there were incidents with paralysis, and release of the vaccine without proper testing, the vaccine still worked.  Polio cases dropped extremely quickly afterwards.  However, this does not necessarily mean the choices the company made were ethical.


### Theranos



![image](https://user-images.githubusercontent.com/66571533/235384841-6d78f226-556e-44f5-b364-48f876b8acfb.png)

* The key concept in the Theranos blood testing machine was the “nanotainer” which would replace the traditional tube after tube of venous blood.
* Rather than collecting blood from a vein in your arm, there would be a finger stick and blood from the finger tip would move into the nonotainer.
* “... a chemistry is performed so that a chemical reaction occurs and generates a signal from the chemical interaction with the sample, which is translated into a result, which is then reviewed by certified laboratory personnel.”
* Most lab results from Theranos’ Arizona labs were off - usually significantly - from testing done several days later at traditional medical labs such as Quest or LabCorp.


#### Notable Individuals



* Whistleblowers:
    * Erika Cheung
    * Tyler Schultz
* Wall Street Journal Reporter
    * John Carreyrou
    * Author of numerous WSJ pieces on Theranos and the book _Bad Blood: Secrets and Lies in a Silicon Valley Startup_
