---
layout: page
title: Kurdistan
header-img: "img/banners/bashur-flag.png"
exclude: true
---

<style>
  .media-icons-&-description{
  }

  .icon-container {
  }

  .description {
    font-style: italic;
  }

  .youtube-icon {
    height: 50px;
    padding-left: 10px;
    margin: auto;
  }

</style>

### Abstract


<i>
This article details a home-built drone that I took to Iraq during the Spring of 2016.&nbsp;  While there, I served as a volunteer in the <a href="https://en.wikipedia.org/wiki/Peshmerga" target="_blank">Kurdish Peshmerga</a> during their war with <a href="https://en.wikipedia.org/wiki/Islamic_State" target="_blank">ISIS</a> during the <a href="https://youtu.be/KbsesrAMjTw" target="_blank">Mosul campaign</a>.&nbsp; My primary mission was to fly recon missions to identify enemy positions within the area of conflict.&nbsp;
</i>

<a href="https://youtu.be/Dy6FYWNopsE" target="_blank">
  <img class="youtube-icon" src="/img/misc/youtube.svg" alt="">
</a>

---
---

In 2013, a group of bad guys with awesome haircuts took over some territory and committed a few [war crimes](https://en.wikipedia.org/wiki/Genocide_of_Yazidis_by_ISIL).&nbsp;  They called themselves the [Islamic State of Iraq and Syria](https://en.wikipedia.org/wiki/Islamic_State_of_Iraq_and_the_Levant), and later the Islamic State.'&nbsp;

At the time, U.S. Government officials were weary of getting into another desert war so they sort-of stayed out of it but at the same time, they were also sort-of involved, albeit in a limited capacity.&nbsp; This lack of full commitment led to a situation in which the local Kurds were left to fend for themselves with limited outside help, and that in turn spurred a volunteer movement of western adventurers who made their way to the Kurdistan region of northern Iraq & Syria.&nbsp;

![snackbars on a soviet APC](https://i.imgur.com/gdJ5YdQ.jpg){:target="_blank"}

Kurdish military commanders were looking for military veterans from NATO member states who possessd specialized skill sets needed in the war effort.&nbsp;  Most such volunteers were former combat medics, while others had combat arms experience.&nbsp;  I was brought on board because I could translate between English and Arabic since Arabic is the defacto lingua franca throughout the conflict zone.

Another reason I came on board was to fly reconnaissance missions with a home built UAV that could fly long distances and be maintained in an austere environment.&nbsp;   I had no such drone so I had to design, test, and build one quickly in a 2 month timeframe.&nbsp;

---

### Design Requirements
The drone itself, along with all tools used to repair it, had to be allowed on international flights (by the TSA) and had to survive warzone conditions.&nbsp;  There would be no clean workspace to make repairs and troubleshoot malfunctions.&nbsp;  We had to assume we would loose at least one drone to enemy fire and be able to build a second one fast, and it had to survive heavy winds and abuse while being transported to different launch sites.&nbsp;

The solution was to refine my [flying crash-test dummy](https://drive.google.com/file/d/1T9fKWgwbUhu5n_UIkCMJMuk2MFkiGEwN/view){:target="_blank"} into something more aerodynamically efficient that could fly long distances.

---

### Introducing the PeshWing
The PeshWing is named after the Kurdish [Peshmerga](https://en.wikipedia.org/wiki/Peshmerga),  the national army of the [Kurdistan Regional Government](https://en.wikipedia.org/wiki/Kurdistan_Regional_Government).&nbsp;  This was a low-cost hack to the problem of how to re-create something like the [RQ-11 Raven UAV system](https://en.wikipedia.org/wiki/AeroVironment_RQ-11_Raven).&nbsp;  The PeshWing could do about 75% of what the Kurds needed the Raven to do, but for a fraction of the price.&nbsp; Below is a one-page bilingual brief for Kurdish commanders to understand the system:

![PeshWing Brief](https://i.imgur.com/fxzw5hW.jpg)

The main idea here was to build an expendable airframe as opposed to a ruggedized one. The wings are made out of 3/16 inch foamcore board and the fuselage is made from 1 inch extruded polystyrene (XPS) board. The entire airframe is composed of modular ‘cuts’ that are made from these materials and those cuts are in turn designed to fit into Tupperware bins that are themselves small enough to fit into airline luggage bags for safe travel to the warzone. In short, this jigsaw-puzzle approach to the airframe design was borne out of logistical considerations more than aerodynamic ones. This modular approach also made field repairs quite easy. The entire thing is put together with hot-glue and packing tape; no bolts, screws, or special tooling are required to build or repair the PeshWing's airframe.&nbsp;

[
![Page 1 of 5 from the PeshWing 2D fab documents](https://i.imgur.com/No09kIi.jpg)
](https://drive.google.com/file/d/1AkJgPMN3NgkpqPPmoYMYnH2lZecQDPwg/view?usp=sharing){:target="_blank"}

The PeshWing can carry one battery for shorter range sorties of 0 to 8 kilometers and two for longer ones exceeding 8 kilometers.&nbsp; With a 2-battery payload it can travel a maximum of 15 kilometers giving it a comfortable 7 kilometer combat radius depending on what the winds are doing.&nbsp;

[
![Fuselage made out of XPS board w/electronics](https://i.imgur.com/qbtPxID.jpg)
](https://drive.google.com/file/d/10ZuGIDeXtm0N71myGmhpH4qinqqLj3C2/view?usp=sharing){:target="_blank"}

The first iteration was back-packable but the folding wings were never employed as we always had vehicle transportation.&nbsp; This let me use the second design iteration featuring my invention that I call ***splats***.&nbsp;

![top perspective of splats](https://i.imgur.com/XIgErRE.jpg)
Splats are a portmanteau that combine the functionality of [spoilers](https://en.wikipedia.org/wiki/Spoiler_%28aeronautics%29){:target="_blank"} and leading edge [slats](https://en.wikipedia.org/wiki/Leading-edge_slat){:target="_blank"} of an aircraft wing.

![side view of airfoil effect w/splats](https://i.imgur.com/4NJJ9EH.jpg)

The splats are deployed for takeoff and landing *(as shown above)* to enable laminar flow on the upper surface of the wing as the wing meets the air at higher angles of attack.&nbsp;  The splats are then retracted once the PeshWing is in level cruising flight *(as shown below)* so as to reduce drag.&nbsp;  The reason this works is because of the small [chord](https://en.wikipedia.org/wiki/Chord_%28aeronautics%29){:target="_blank"} length between the leading & training edges of the aircraft.&nbsp;  When the PeshWing comes in for an aggressive combat landing, the splats are deployed as airbrakes that enable steep descent without over-speeding.&nbsp;  For reasons beyond this photo essay, splats would not work on a larger, manned aircraft, but they *do* work on smaller, hand-held aircraft.&nbsp;

![side view with splats retracted](https://i.imgur.com/hSWj34T.jpg)

The camera gimbal was designed to be 3D printed and it has a one-axis pan.&nbsp;  It uses the same servo type as the wing elevons & wing splats, and although this arrangement is a bit heavy, the servo redundancy means any spare servo can be used to replace any servo that has gone bad on the PeshWing.&nbsp;

![1-axis 3D printed GoPro camera gimbal](https://i.imgur.com/EQrKTh3.jpg)

Deploying with a fully rendered set of schematics allowed for easy maintenance & repair.&nbsp; Avionics systems and subsystems were chosen for reliability over capability and cost.&nbsp;  Multiple camera systems could capture photos and video and varying angles on the same sortie.&nbsp;

![schematic wiring diagram](https://i.imgur.com/EDh9vEP.jpg)

![three amigos w/ PeshWing drone](https://i.imgur.com/jyervAf.jpg)

The PeshWing needs to be launched with a bungee when carrying two batteries, and can be hand-launched when taking off with just one battery.

![bungee launch of a drone](https://i.imgur.com/dqKiR2T.jpg)

The PeshWing's main mission was to scout out ISIS positions in the myriad of abandoned villages covering northern Iraq.

![a view from the drone](https://i.imgur.com/iPGHhj2.jpg)

The PeshWing also provided real-time intelligence for fire support missions.&nbsp;  Here we are on the front-line berm scouting out enemy positions from the air and ground:

![on the berm looking for the enemy](https://i.imgur.com/3azmhRK.jpg)

Our favorite people to work with are field artillery people.

![120mm Mortar Fire](https://i.imgur.com/yI8huJC.jpg)

### First Aid Medical Training
Whenever we weren't in the air, we were teaching first aid classes to Peshmerga soldiers at different locations across the battlefront.&nbsp;  Here we have some Kurdish Peshmergas learning the basics while I give the lesson in Arabic.&nbsp;  My Arabic-to-Kurdish translator got a kick out of my accent and we all had a good time learning:  

![Me approaching a notionally injured Peshmerga](https://i.imgur.com/uyqs4wl.jpg)

Our team of NATO veterans were invited by the Kurdistan Regional Government's Ministry of Health which ran our training program and issued graduation certificates to Kurdish students who completd the course.&nbsp;  Here is graduation day for cohort 3:

![Peshmerga class cohort graduation](https://i.imgur.com/XJTBHws.jpg)

Kurdistan (K24) cable news came out to film our final training exercise and see what we were up to.

![Kurdish news anchor](https://i.imgur.com/T7JFS7c.jpg)

Hi mom, I'm on TV!
