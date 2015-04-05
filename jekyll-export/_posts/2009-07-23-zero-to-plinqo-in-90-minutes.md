---
title: Zero to Plinqo in 90 minutes
author: kellyorr
layout: post
permalink: /zero-to-plinqo-in-90-minutes/
categories:
  - Software Development
tags:
  - Database
  - ORM
---
****[<img class="alignleft size-full wp-image-30" title="CodesmithTools" src="http://www.continuousrefactor.com/wp-content/uploads/2011/01/CodesmithTools.jpg" alt="" width="103" height="38" hspace="5" />][1][Plinqo][2] is a collection of CodeSmith templates designed to work with LINQ to SQL.  Here are the steps I took to go from knowing very little about Plinqo to being ready to implement in my next development project.  
1) Download a [CodeSmith Trial][3]  
2) Install CodeSmith  
3) Download [Plinqo][4]  
4) Watch 16 minute [Quick Start video][5] See notes below.  
5) Watch 22 minute [Feature Overview video][6] See notes below.

**Quick Start Video Notes**

  * Plinqo provides DBML, business entities, and manager/queries.
  * Running the quick start generates three projects: Data, Test and UI.
  * In the Data project there a .dbml file is generated along with /entities/ in single files and /managers/ folders.
  * To use the Plinqo gernated projects in your project just add references to CodeSmith.Data and the auto-geneated .Data.

**Feature O****verview Video**

  * The DBML inherits database schema changes
  * The DBML persists changes to DBML mappings
  * Meta data updates are perserved through merging
  * Plinqo can be used to create a powerful business rules engine

Plinqo overs a lot of automated horsepower in wiring up database schema to business objects.  Templates can be generated in both C# and VB.

 [1]: http://www.continuousrefactor.com/wp-content/uploads/2011/01/CodesmithTools.jpg
 [2]: http://www.plinqo.com
 [3]: http://www.codesmithtools.com/requesttrial/18
 [4]: http://plinqo.com/Download.ashx
 [5]: http://www.codesmithtools.com/video/plinqo-part-1-quick-start.html
 [6]: http://www.codesmithtools.com/video/plinqo-part-2-feature-overview.html