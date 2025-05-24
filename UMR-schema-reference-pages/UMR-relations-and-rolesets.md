<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>My New Page</title>
  <style>
    body {
      font-family: sans-serif;
      max-width: 800px;
      margin: 2em auto;
      padding: 1em;
      line-height: 1.6;
    }
    .box {
      background-color: #e6f2ff;
      padding: 0.5em;
      border-radius: 6px;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 2em;
    }
    th, td {
      border: 1px solid #ccc;
      padding: 0.5em;
      text-align: left;
      vertical-align: top;
    }
    th {
      background-color: #f0f0f0;
    }
    td:nth-child(1), td:nth-child(2), td:nth-child(3) {
      line-height: 1;
    }
    td:nth-child(4), td:nth-child(5),
    th:nth-child(4), th:nth-child(5){
      white-space: normal;
      width: auto;
    }
    .highlight {
      background-color: #e6f2ff;
      border-radius: 4px;
      padding: 0.1em 0.3em;
      display: inline-block;
      position: relative;
      font-family: inherit;
      font-size: inherit;
    }
    .popup {
      display: none;
      position: absolute;
      top: 120%;
      left: 0;
      padding: 0.5em;
      background: white;
      border: 1px solid #ccc;
      box-shadow: 0 0 10px rgba(0,0,0,0.3);
      z-index: 1000;
      width: max-content;
      white-space: pre-wrap;
      font-family: monospace;
      font-style: normal;
    }
    .highlight:hover .popup ,
    .exsent:hover .popup {
      display: block;
    }
    .indent {
      display: block;
      margin-left: 1em;
      font-family: monospace;
      font-size: inherit;
    }
    .exsent {
      display: block;
      margin-left: 1em;
      font-family: inherit;
      font-size: inherit;
      font-style: italic;
      position: relative;
    }
    .definition {
      white-space: normal;
      width: auto;
      line-height: 1.2;
    }
    .nowrap {
      white-space: nowrap;
    }

  </style>
</head>
<body>


<h1>UMR Relations & Rolesets</h1>

<p>This is a reference page with lists of UMR participant roles, non-participant roles, and attribute roles, along with their inverse forms and reifications. Examples are given in English with English PropBank roleset labels (for sense disambiguation), but without the numbered args associated with the rolesets. </p>

<h2>Participant Roles</h2>
<p>These roles are central to events</p>

<table>
  <thead>
    <tr>
      <th>Role</th>
      <th>Inverse</th>
      <th>Reification</th>
      <th>Definition</th>
    </tr>
  </thead>
  
  <tbody>
    <tr>
      <td>
        <span class="highlight"><code>:actor</code>
          <span class="popup"><em>Ex:</em> <strong>He</strong> ate the corn.
    (e / eat-01
        <strong>:actor (p / person
            :refer-person 3rd
            :refer-number singular)</strong>
        :undergoer (c / corn)
        :aspect performance
        :modal-strength full-affirmative)
      </td>
      <td>
        <span class="highlight">
          <code>:actor-of</code>
          <span class="popup"><em>Ex:</em> <strong>the boy</strong> who ate the corn
    <strong>(b / boy
        :actor-of</strong> (e / eat-01
            :undergoer (c / corn)
            :aspect performance
            :modal-strength full-affirmative))
      </td>
      <td>
        <span class="highlight">
          <code>have-actor-91</code><br>
          <span class="indent">:ARG1 event<br> 
            :ARG2 actor
      </td>
      <td class="definition">Animate entity that initiates the action.<br>
        <span class="exsent"><strong>The doctor</strong> laughed.
          <span class="popup">(l / laugh-01
  :actor (d / doctor)
  :aspect performance
  :modal-strength full-affirmative)</span></span>
        <span class="exsent"><strong>The doctor</strong> ate a salad.
          <span class="popup">(e / eat-01
  <strong>:actor (d / doctor)</strong>
  :undergoer (s / salad)
  :aspect performance
  :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:co-actor</code>
          <span class="popup"><em>Ex:</em> I was arguing with <strong>him</strong>.
    (a / argue-01
        :actor (p / person
            :refer-person 1st
            :refer-number singular)
        <strong>:co-actor (p2 / person
            :refer-person 3rd
            :refer-number singluar)</strong>
        :aspect activity
       :modal-strength full-affirmative)
      </td>
      <td>
        <span class="highlight">
          <code>:co-actor-of</code>
          <span class="popup"><em>Ex:</em> <strong>the man</strong> I was arguing with
    <strong>(m / man
        :co-actor-of</strong> (a / argue-01
            :actor (p2 / person
               :refer-person 1st
               :refer-number singular)
           :aspect activity
           :modal-strength full-affirmative))
      </td>
      <td>
        <span class="highlight">
          <code>have-co-actor-91</code><br>
          <span class="indent">:ARG1 event<br> 
            :ARG2 co-actor
      </td>
      <td class="definition">Secondary parallel Actor who is acting independently of the primary <span class="highlight">:actor</span>.<br>
        <span class="exsent">James battled <strong>the dragon</strong>.
          <span class="popup">(b / battle-01
    :actor (p / person
        :name (n / name :op1 "James"))
    <strong>:co-actor (d / dragon)</strong>
    :aspect activity
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:undergoer</code>
          <span class="popup"><em>Ex:</em> He ate <strong>the corn</strong>.
    (e / eat-01
        :actor (p / person
            :refer-person 3rd
            :refer-number singular)
        <strong>:undergoer (c / corn)</strong>
        :aspect performance
        :modal-strength full-affirmative)
      </td>
      <td>
        <span class="highlight">
          <code>:undergoer-of</code>
          <span class="popup"><em>Ex:</em> <strong>the corn</strong> the boy ate
    <strong>(c / corn
       :undergoer-of</strong> (e / eat-01
            :actor (b / boy)
            :aspect performance
           :modal-strength full-affirmative))
      </td>
      <td>
        <span class="highlight">
          <code>have-undergoer-91</code><br>
          <span class="indent">:ARG1 event<br> 
            :ARG2 undergoer
      </td>
      <td class="definition">Entity (animate or inanimate) that is affected by the action.<br>
        <span class="exsent"><strong>The papers </strong> burned.
          <span class="popup">(b / burn-01
    <strong>:undergoer (p / paper
        :refer-number plural)</strong>
    :aspect activity
    :modal-strength full-affirmative)</span></span>
        <span class="exsent">He burned <strong>the onions</strong>.
          <span class="popup">(b / burn-01
    :actor (p / person
        :refer-person 3rd
        :refer-number singular)
    <strong>:undergoer (o / onion
        :refer-number plural)</strong>
    :aspect performance
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:theme</code>
          <span class="popup"><em>Ex:</em> She put <strong>the books</strong> on the shelf.
    (p / put-01
        :actor (p2 / person
            :refer-person 3rd
            :refer-number singular)
        <strong>:theme (b / book
            :refer-number plural)</strong>
        :goal (s / shelf)
        :aspect performance
        :modal-strength full-affirmative)
      </td>
      <td>
        <span class="highlight">
          <code>:theme-of</code>
          <span class="popup"><em>Ex:</em> <strong>the books</strong> she had put on the shelf
    <strong:source (b / book
        :refer-number plural
        :theme-of></strong> (p2 / put-01
            :actor (p3 / person
                :refer-person 3rd
                :refer-number singular)
            :goal (s / shelf)
            :aspect performance
            :modal-strength full-affirmative))
      </td>
      <td>
        <span class="highlight">
          <code>have-theme-91</code><br>
          <span class="indent">:ARG1 event<br> 
            :ARG2 theme
      </td>
      <td class="definition">Entity (animate, inanimate, or abstract) that moves from one entity to another entity, either spatially or metaphorically.<br>
        <span class="exsent">She put <strong>the books</strong> on the shelf.
          <span class="popup">(p / put-01
    :actor (p / person
        :refer-person 3rd
        :refer-number singular)
    <strong>:theme (b / book
        :refer-number plural)</strong>
    :aspect performance
    :modal-strength full-affirmative)</span></span>
        <span class="exsent">She tore <strong>a page</strong> from the book.
          <span class="popup">(t /tear-01
    :actor (p / person
        :refer-person 3rd
        :refer-number singular)
    <strong>:theme (p2 / page
        :refer-number singular)</strong>
    :source (b / book
        :refer-number plural)
    :aspect performance
    :modal-strength full-affirmative)</span></span>
        <span class="exsent">He gave me <strong>a sandwich</strong>.
          <span class="popup">(g / give-01
    :actor (p / person
        :refer-person 3rd
        :refer-number singular)
    <strong>:theme (s / sandwich
        :refer-number singular)</strong>
    :recipient (p2 / person
        :refer-person 1st
        :refer-number singular)
    :aspect performance
    :modal-strength full-affirmative)</span></span>
        <span class="exsent">She told him <strong>a story</strong>.
          <span class="popup">(t / tell-01
    :actor (p / person
        :refer-person 3rd
        :refer-number singular)
    <strong>:theme (s / story
        :refer-number singular)</strong>
    :recipient (p2 / person
        :refer-person 3rd
        :refer-number singular)
    :aspect performance
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:recipient</code>
          <span class="popup"><em>Ex:</em> I gave <strong>Martha</strong> a book.
    (g / give-01
        :actor (p / person
            :refer-person 1st
            :refer-number singular)
        <strong>:recipient (p2 / person :name (n / name :op1 "Martha"))</strong>
        :theme (b / book)
        :aspect performance
        :modal-strength full-affirmative)
      </td>
      <td>
        <span class="highlight">
          <code>:recipient-of</code>
          <span class="popup"><em>Ex:</em> <strong>The book</strong> I gave Martha was old.
    (h / have-age-91
        :ARG1 <strong>(b / book
            :theme-of</strong> (g / give-01
                :actor (p / person
                    :refer-person 1st
                    :refer-number singular)
                :recipient (p2 / person :name (n / name :op1 "Martha"))
                :aspect performance
                :modal-strength full-affirmative))
        :ARG2 (o / old)
      </td>
      <td>
        <span class="highlight">
          <code>have-recipient-91</code><br>
          <span class="indent">:ARG1 event<br> 
            :ARG2 recipient
      </td>
      <td class="definition">Animate entity that gains possession (or at least temporary control) of another entity.
        <span class="exsent">He gave <strong>me</strong> a sandwich.
          <span class="popup">(g / give-01
    :actor (p / person
        :refer-person 3rd
        :refer-number singular)
    :theme (s / sandwich
        :refer-number singular)
    <strong>:recipient (p2 / person
        :refer-person 1st
        :refer-number singular)</strong>
    :aspect performance
    :modal-strength full-affirmative)</span></span>
        <span class="exsent">She told <strong>him</strong> a story.
          <span class="popup">(t / tell-01
    :actor (p / person
        :refer-person 3rd
        :refer-number singular)
    :theme (s / story
        :refer-number singular)
    <strong>:recipient (p2 / person
        :refer-person 3rd
        :refer-number singular)</strong>
    :aspect performance
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:force</code>
          <span class="popup"><em>Ex:</em> <strong>The storm</strong> damaged the power lines.
    (d/ damage-01 
        <strong>:force (s/ storm)</strong>  
        :undergoer (l/ line
            :purpose (p/ power)
            :refer-number plural)
        :aspect performance
        :modal-strength full-affirmative)</span></span>
      </td>
      <td>
        <span class="highlight">
          <code>:force-of</code>
          <span class="popup"><em>Ex:</em> <strong>the storm</strong> that damaged the power lines
    <strong>(s/ storm
        :force-of</strong> (d/ damage-01   
            :undergoer (l/ line
                :purpose (p/ power)
                :refer-number plural)
          	:aspect performance
          	:modal-strength full-affirmative))</span></span>
      </td>
      <td>
        <span class="highlight">
          <code>have-force-91</code><br>
          <span class="indent">:ARG1 event<br> 
            :ARG2 force
      </td>
      <td class="definition">Inanimate entity that initiates the action.
        <span class="exsent"><strong>The wind</strong> knocked down the tree.
          <span class="popup">(k / knock-down-02
    <strong>:force (w / wind)</strong>
    :undergoer (t / tree)
    :aspect performance
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:causer</code>
          <span class="popup"><em>Ex:</em>
    <strong>Parte</strong>   in    Cinte a         hni-<strong>ter</strong>  
    <strong>Parte</strong>   ERG   Cinte 3SG.NOM   laugh.1-<strong>CAUS</strong>  
    ‘Parte made Cinte laugh.’<br>
    (h/ hniter-00 ‘make laugh’ 
        <strong>:causer (p/ person
            :name (n/ name :op1 "Parte"))</strong> 
        :actor (p2/ person
            :name (n2/ name :op1 "Cinte"))  
        :aspect performance
        :modal-strength full-affirmative)
      </td>
      <td>
        <span class="highlight">
          <code>:causer-of</code>
          <span class="popup"><em>Ex:</em> <strong></strong><br>
          
        </td>
      </td>
      <td>
        <span class="highlight">
          <code>have-causer-91</code><br>
          <span class="indent">:ARG1 event<br> 
            :ARG2 causer
      </td>
      <td class="definition">Animate entity that acts on another animate entity to initiate the action.<br>
        <span class="exsent"><strong>The mother</strong> made her child eat the broccoli.
          <span class="popup">(m / make-01
    <strong>:causer (p / person
        :ARG1-of (h / have-rel-role-91
            :ARG2 (p2 / person)
            :ARG3 (m / mother)
            :ARG4 (c / child)))</strong>
    :theme (e / eat-01
        :actor p2
        :undergoer (b / broccoli)
    :aspect performance
    :modal-strength full-affirmative))</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:experiencer</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td class="nowrap">
        <span class="highlight">
          <code>:experiencer-of</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td rowspan="2" class="nowrap">
        <span class="highlight">
          <code>have-experience-91</code><br>
          <span class="indent">:ARG1 experiencer<br> 
            :ARG2 the experience<br> 
            :ARG3 stimulus<br> 
            :ARG4 the event, if separate
      </td>
      <td class="definition">Animate entity that cognitively or sensorily experiences a stimulus.
        <span class="exsent"><strong>The dog</strong> heard a sound.
          <span class="popup">(h / hear-01
    <strong>:experiencer (d / dog)</strong>
    :stimulus (s / sound)
    :aspect performance
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:stimulus</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>:stimulus-of</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td class="definition">Entity (animate or inanimate) that is experienced by an <span class="highlight">:experiencer</span><br>
        <span class="exsent">The dog heard <strong>a sound</strong>.
          <span class="popup">(h / hear-01
    :experiencer (d / dog)
    <strong>:stimulus (s / sound)</strong>
    :aspect performance
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:instrument</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>:instrument-of</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>have-instrument-91</code><br>
          <span class="indent">:ARG1 event<br> 
            :ARG2 instrument
      </td>
      <td class="definition">Inanimate entity that is manipulated by an external Causer in order to initiate the action.<br>
        <span class="exsent">She hit him with <strong>a broom</strong>. 
          <span class="popup">(h / hit-01
    :actor (p / person
        :refer-person 3rd
        :refer-number singular)
    :undergoer (p2 / person
        :refer-person 3rd
        :refer-number singular)
    <strong>:instrument (b / broom)</strong>
    :aspect performance
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:companion</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>:companion-of</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>have-companion-91</code><br>
          <span class="indent">:ARG1 event<br> 
            :ARG2 companion
      </td>
      <td class="definition">Animate entity that acts with the actor to initiate the action.<br>
        <span class="exsent">He cooked dinner with <strong>his wife</strong>. 
          <span class="popup">(c / cook-01
    :actor (p / person
        :refer-person 3rd
        :refer-number singular)
    :undergoer (d / dinner)
    <strong>:companion (p2 / person
        :refer-person 3rd
        :refer-number singular)</strong>
    :aspect performance
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:material</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>:material-of</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>have-material-91</code><br>
          <span class="indent">:ARG1 event<br> 
            :ARG2 material
      </td>
      <td class="definition">Entity (inanimate) that is transformed into a new entity.
        <span class="exsent">He made a roux with <strong>flour and butter</strong>.  
          <span class="popup">(m / make-01
    :actor (p / person
        :refer-person 3rd
        :refer-number singular)
    :undergoer (r / roux)
    <strong>:material (a / and
        :op1 (f / flour)
        :op2 (b / butter))</strong>
    :aspect performance
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:source</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>:source-of</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>have-source-91</code><br>
          <span class="indent">:ARG1 event<br> 
            :ARG2 source
      </td>
      <td class="definition">Entity from which the <span class="highlight">:theme</span> detaches.
        <span class="exsent">He plucked a flower from <strong>the bush</strong>.   
          <span class="popup">(p / pluck-01
    :actor (p2 / person
        :refer-person 3rd
        :refer-number singular)
    :theme (f / flower)
    <strong>:source (b / bush)</strong>
    :aspect performance
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:place</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>:place-of</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>have-place-91</code><br>
          <span class="indent">:ARG1 event<br> 
            :ARG2 place
      </td>
      <td class="definition">Location at which the action takes place.
        <span class="exsent">He read a book <strong>in the garden</strong>.   
          <span class="popup">(r / read-01
    :actor (p2 / person
        :refer-person 3rd
        :refer-number singular)
    :theme (b / book)
    <strong>:place (g / garden)</strong>
    :aspect performance
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:start</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>:start-of</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>have-start-91</code><br>
          <span class="indent">:ARG1 event<br> 
            :ARG2 start
      </td>
      <td class="definition">Location at which a motion event begins.
        <span class="exsent">She biked <strong>from her house</strong>.    
          <span class="popup">(b / bike-01
    :actor (p2 / person
        :refer-person 3rd
        :refer-number singular)
    <strong>:start (h / house
        :possessor p2)</strong>
    :aspect performance
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
    <tr>
      <td><span class="highlight">
        <code>:goal</code>
        <span class="popup"><em>Ex:</em> <strong></strong>
        
      </td>
      <td>
        <span class="highlight">
          <code>:goal-of</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>have-goal-91</code><br>
          <span class="indent">:ARG1 event<br> 
            :ARG2 goal
      </td>
      <td class="definition">Location at which the action ends, the end point at which the theme arrives.
        <span class="exsent">She put the books <strong>on the shelf</strong>.  
          <span class="popup">(p / put-01
    :actor (p2 / person
        :refer-person 3rd
        :refer-number singular)
    :theme (b / book
        :refer-number plural)
    <strong>:goal (s / shelf)</strong>
    :aspect performance
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:affectee</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>:affectee-of</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>have-affectee-91</code><br>
          <span class="indent">:ARG1 event<br> 
            :ARG2 affectee
      </td>
      <td class="definition">Animate entity which the action has a positive or negative influence on, i.e. beneficiary or maleficiary.<br>
        <span class="exsent">He made a cake for<strong>the dog</strong>.
          <span class="popup">(m / make-01
    :actor (p2 / person
        :refer-person 3rd
        :refer-number singular)
    :theme (c / cake)
    <strong>:affectee (d / dog)</strong>
    :aspect performance
    :modal-strength full-affirmative)</span></span>
        <span class="exsent">She twisted his words <strong>against him</strong>.
          <span class="popup">(t / twist-01
    :actor (p2 / person
        :refer-person 3rd
        :refer-number singular)
    :theme (w / word
        :refer-number plural
        :possessor (p / person
            :refer-person 3rd
            :refer-number singular)
    <strong>:affectee p</strong>
    :aspect performance
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:cause</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>:cause-of</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>have-cause-91</code><br>
          <span class="indent">:ARG1 event<br> 
            :ARG2 cause
      </td>
      <td class="definition">Inanimate entity that causes the action to happen.
        <span class="exsent">He was late because of <strong>the fire</strong>.
          <span class="popup">(l / late-02
    :theme (p2 / person
        :refer-person 3rd
        :refer-number singular)
    <strong>:cause (f / fire-05
        :aspect process
        :modal-strength full-affirmative)</strong>
    :aspect performance
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:manner</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>:manner-of</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>have-manner-91</code><br>
          <span class="indent">:ARG1 event<br> 
            :ARG2 manner
      </td>
      <td class="definition">Manner in which the action takes place.
        <span class="exsent">She exercised by<strong>lifting weights</strong>.
          <span class="popup">(e / exercise-01
    :actor (p / person
        :refer-person 3rd
        :refer-number singular)
    <strong>:manner (l / lift-01
        :actor p 
        :theme (w / weight
            :refer-number plural)
        :aspect performance
        :modal-strength full-affirmative)</strong>
    :aspect performance
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:reason</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>:reason-of</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>have-reason-91</code><br>
          <span class="indent">:ARG1 event<br> 
            :ARG2 reason
      </td>
      <td class="definition">Motivation for the <span class="highlight">:actor</span> to initiate the action.
        <span class="exsent">They got married because <strong>they were in love</strong>.
          <span class="popup">(m / marry-01
    :actor (p / person
        :refer-person 3rd
        :refer-number plural)
    <strong>:reason (l / love-01
        :actor p 
        :aspect state
        :modal-strength full-affirmative)</strong>
    :aspect performance
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:purpose</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>:purpose-of</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>have-purpose-91</code><br>
          <span class="indent">:ARG1 event<br> 
            :ARG2 purpose
      </td>
      <td class="definition">Intended event that results from the action.
        <span class="exsent">They dropped water in order to <strong>fight fires</strong>.
          <span class="popup">(d / drop-01
    :actor (p / person
        :refer-person 3rd
        :refer-number plural)
    :theme (w / water)
    <strong>:purpose (f / fight-01
        :actor p 
        :force (f2 / fire-05
            :refer-number plural
            :aspect process)
        :aspect habitual
        :modal-strength partial-affirmative)</strong>
    :aspect habitual
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:result</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>:result-of</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>have-result-91</code><br>
          <span class="indent">:ARG1 event<br> 
            :ARG2 result
      </td>
      <td class="definition">Event or state that comes about in some way that is contingent on another event.
        <span class="exsent">She worked her fingers <strong>raw</strong>.
          <span class="popup">(w / work-10
    :actor (p / person
        :refer-person 3rd
        :refer-number singular)
    :undergoer (f / finger
        :part-of p 
        :refer-number plural)
    <strong>:result (r / raw-01
        :theme f
        :aspect state
        :modal-strength full-affirmative)</strong>
    :aspect performance
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:temporal</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>:temporal-of</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>have-temporal-91</code><br>
          <span class="indent">:ARG1 event<br> 
            :ARG2 temporal
      </td>
      <td class="definition">Element (event or time expression) that has a temporal relation with the action.
        <span class="exsent">She left <strong>after dinner</strong>.
          <span class="popup">(l / leave-11
    :actor (p / person
        :refer-person 3rd
        :refer-number singular)
    <strong>:temporal (a / after
        :op1 (d / dinner))</strong>
    :aspect performance
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:extent</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>:extent-of</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>have-extent-91</code><br>
          <span class="indent">:ARG1 event<br> 
            :ARG2 extent
    </td>
      <td class="definition">Measurement phrase.
        <span class="exsent">He ran <strong>7 miles</strong>.
          <span class="popup">(r / run-02
    :actor (p / person
        :refer-person 3rd
        :refer-number singular)
    <strong>:extent (d / distance-quantity
        :quant 7
        :unit (m / mile))</strong>
    :aspect performance
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:other-role</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>:other-role-of</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>have-other-role-91</code><br>
          <span class="indent">:ARG1 event<br> 
            :ARG2 other role
      </td>
      <td class="definition">This role can be used when an annotator is unsure of which role is appropriate.<br></td>
    </tr>
  </tbody>
</table>


<h2>Non-Participant Roles</h2>
<p>These roles are less central to events than participant roles. Some may modify entities as well as events.</p>

<table>
  <thead>
    <tr>
      <th>Role</th>
      <th>Inverse</th>
      <th>Reification</th>
      <th>Definition</th>
    </tr>
  </thead>
  
  <tbody>
    <tr>
      <td>
        <span class="highlight">
          <code>:direction</code>
          <span class="popup"><em>Ex:</em> Move that block <strong>the other way</strong>
    (m / move-01 
        :mode imperative
        :actor (p / person
            :refer-person 2nd
            :refer-number singular)
        :theme (b / block
            :mod (t / that))
        <strong>:direction (w / way
                :mod-of (o / other-01))</strong>
        :aspect performance
        :modal-strength partial-affirmative)
      </td>
      <td>
        <span class="highlight">
          <code>:direction-of</code>
          <span class="popup"><em>Ex:</em>
          
      </td>
      <td>
        <span class="highlight">
          <code>have-direction-91</code><br>
          <span class="indent">:ARG1 event<br> 
            :ARG2 direction
      </td>
      <td class="definition">Direction of motion event.
        <span class="exsent">He drove <strong>west</strong>.
          <span class="popup">(d / drive
    :actor (p / person
        :refer-person 3rd
        :refer-number singular)
    <strong>:direction (t / trajectory
        :direction-of (w / west-01))</strong>
    :aspect activity
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:path</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>:path-of</code>
          <span class="popup"><em>Ex:</em>
          
      </td>
      <td>
        <span class="highlight">
          <code>have-path-91</code><br>
          <span class="indent">:ARG1 event/entity<br> 
            :ARG2 path
      </td>
      <td class="definition">Path of motion event.
        <span class="exsent">I walked <strong>the track</strong> at the highschool.
          <span class="popup">(w / walk-01
    :actor (p / person
        :refer-person 1st
        :refer-number singular)
    <strong>:path (t / track)</strong>
    :place (h / highschool)
    :aspect activity
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:quant</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>:quant-of</code>
          <span class="popup"><em>Ex:</em>
          
      </td>
      <td>
        <span class="highlight">
          <code>have-quant-91</code><br>
          <span class="indent">:ARG1 entity<br> 
            :ARG2 quant
      </td>
      <td class="definition">Quantity of an entity.
        <span class="exsent">My brother has <strong>12</strong> pets.
          <span class="popup">(h / have-91
    :ARG1 (p / person
        :ARG1-of (h2 / have-rel-role-91
            :ARG2 (p / person
                :refer-person 1st
                :refer-number singular)
            :ARG3 (b / brother)))
    :ARG2 (p2 / pet
        <strong>:quant 12</strong>)
    :aspect state
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:duration</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>:duration-of</code>
          <span class="popup"><em>Ex:</em>
          
      </td>
      <td>
        <span class="highlight">
          <code>have-duration-91</code><br>
          <span class="indent">:ARG1 event<br> 
            :ARG2 duration
      </td>
      <td class="definition">Duration of an event.
        <span class="exsent">The commencement ceremony went on <strong>for 4 hours</strong>.
          <span class="popup">(g / go-on-15
    :theme (c / ceremony-01
        :purpose (c2 / commencement)
        :aspect process
        :modal-strength full-affirmative)
    :duration <strong>(t / temporal-quantity
        :quant 4 
        :unit (h2 / hour))</strong>
    :aspect performance
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:frequency</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>:frequency-of</code>
          <span class="popup"><em>Ex:</em>
          
      </td>
      <td>
        <span class="highlight">
          <code>have-frequency-91</code><br>
          <span class="indent">:ARG1 event<br> 
            :ARG2 frequency
      </td>
      <td class="definition">How often an event occurs.
        <span class="exsent">My dog runs around the yard <strong>whenever it rains</strong>.
          <span class="popup">(r / run-02
    :actor (d / dog
        :possessor (p / person
            :refer-person 1st
            :refer-number singular))
    :path (a / around
        :op1 (y / yard))
    :frequency <strong>(r2 / rate-entity-91
        :ARG4 (r3 / rain-01
            :aspect performance
            :modal-strength partial-affirmative))</strong>
    :aspect habitual
    :modal-strength full-affirmative)</span></span>
        <span class="exsent">My cat hit my dog on the nose <strong>3 times</strong>.
          <span class="popup">(h / hit-01
    :actor (c / cat
        :possessor (p / person
            :refer-person 1st
            :refer-number singular))
    :undergoer (d / dog
        :possessor p)
    :place (n / nose
        :part-of d)
    <strong>:frequency 3</strong>
    :aspect performance
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:mod</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>:mod-of</code>
          <span class="popup"><em>Ex:</em>
          
      </td>
      <td>
        <span class="highlight">
          <code>have-mod-91</code><br>
          <span class="indent">:ARG1 entity<br> 
            :ARG2 modifier
      </td>
      <td class="definition">For generic modifiers of entities and events.<br>
        <span class="exsent">I don't want to wear <strong>those</strong> shoes.
          <span class="popup">(w / want-01
    :polarity -
    :experiencer (p / person
        :refer-person 1st
        :refer-number singular)
    :stimulus (w2 / wear-01
        :actor p 
        :theme (s / shoe 
            :refer-number plural
            <strong>:mod (t / that)</strong>)
        :aspect state
        :modal-strength partial-negative
        :modal-predicate w)
    :aspect state
    :modal-strength full-negative)</span></span>
        <span class="exsent">The <strong>tall</strong> man reached the mayonnaise for me.
          <span class="popup">(r / reach-01
    :actor (m / man
        <strong>:mod (t / tall))</strong>
    :theme (m2 / mayonnaise)
    :affectee (p / person
        :refer-person 1st
        :refer-number singular)
    :aspect performance
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:topic</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>:topic-of</code>
          <span class="popup"><em>Ex:</em>
          
      </td>
      <td>
        <span class="highlight">
          <code>have-topic-91</code><br>
          <span class="indent">:ARG1 event/entity<br> 
            :ARG2 topic
      </td>
      <td class="definition">The subject matter of an event or entity.
        <span class="exsent">The cobbler wrote a book <strong>about shoes</strong>.
          <span class="popup">(w / write-01
    :actor (p / person
        :ARG1-of (h / have-role-91
            :ARG2 (c / cobbler)))
    :theme (b / book
        <strong>:topic (s / shoe
            :refer-number plural)</strong>)
    :aspect performance
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:vocative</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>:vocative-of</code>
          <span class="popup"><em>Ex:</em>
          
      </td>
      <td>
        <span class="highlight">
          <code>have-vocative-91</code><br>
          <span class="indent">:ARG1 event<br> 
            :ARG2 person addressed
      </td>
      <td class="definition">Within utterances, when the addressee is called out.
        <span class="exsent">"Good morning, <strong>Bert</strong>."
          <span class="popup">(s / say-91
    :ARG1 (g / good-02
        :theme (m / morning)
        <strong>:vocative (p / person 
            :name (n / name :op1 "Bert"))</strong>
        :aspect state
        :modal-strength full-affirmative
        :quote s)
    :ARG2 p)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:medium</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>:medium-of</code>
          <span class="popup"><em>Ex:</em>
          
      </td>
      <td>
        <span class="highlight">
          <code>have-medium-91</code><br>
          <span class="indent">:ARG1 event/entity<br> 
            :ARG2 medium
      </td>
      <td class="definition">The medium through which an event is carried out.
        <span class="exsent">I called my mother <strong>on the phone</strong>.
          <span class="popup">(c / call-02
    :actor (p / person
        :refer-person 1st
        :refer-number singular)
    :theme (p2 / person
        :ARG1-of (h / have-rel-role-91
            :ARG2 (p3 / person)
            :ARG3 (m / mother)))
    <strong>:medium (p4 / phone)</strong>
        :aspect performance
        :modal-strength full-affirmative)</span></span>
        <span class="exsent">a <strong>French</strong> song
          <span class="popup">(s / song
    <strong>:medium (l / language</strong>
        :name (n / name :op1 "French")))</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:possessor</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>:possessor-of</code>
          <span class="popup"><em>Ex:</em>
          
      </td>
      <td>
        <span class="highlight">
          <code>have-poss-91</code><br>
          <span class="indent">:ARG1 possessed entity<br> 
            :ARG2 possessor
      </td>
      <td class="definition">The entity who has possession (or temporary control) over something.
        <span class="exsent"><strong>His</strong> shoes are on the floor.
          <span class="popup">(h / have-place-91
    :ARG1 (s / shoe
        :refer-number plural
        <strong>:possessor (p / person
            :refer-person 3rd
            :refer-number singular))</strong>
    :ARG2 (f / floor)
    :aspect state
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:part</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>:part-of</code>
          <span class="popup"><em>Ex:</em>
          
      </td>
      <td>
        <span class="highlight">
          <code>have-part-91</code><br>
          <span class="indent">:ARG1 whole entity<br> 
            :ARG2 part
      </td>
      <td class="definition">A component part of a whole.
        <span class="exsent">My <strong>nose</strong> itched.
          <span class="popup">(i / itch-01
    :experiencer (n / nose
        <strong>:part-of (p / person
            :refer-person 1st
            :refer-number singular))</strong>
    :aspect state
    :modal-strength full-affirmative)</span></span>
        <span class="exsent">The movers lay the box on its <strong>side</strong>.
          <span class="popup">(l / lay-01
    :actor (p / person
        :refer-number plural
        :actor-of (m / move-01))
    :theme (b / box)
    :orientation (o / on-04
        :theme b 
        :part (s / side
        <strong>:part-of b)</strong>
    :aspect performance
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:group</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight">
          <code>:group-of</code>
          <span class="popup"><em>Ex:</em>
          
      </td>
      <td>
        <span class="highlight">
          <code>have-group-91</code><br>
          <span class="indent">:ARG1 members<br> 
            :ARG2 group
      </td>
      <td class="definition">For set/member relationships.
        <span class="exsent"><strong>a swarm</strong> of bees
          <span class="popup"><strong>(s / swarm
    :group-of</strong> (b / bee
        :refer-number plural))</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight"><code>:age</code>
          <span class="popup"><em>Ex:</em> <strong></strong>.
          
      </td>
      <td>
        <span class="highlight"><code>:age-of</code>
          <span class="popup"><em>Ex:</em>
          
      </td>
      <td>
        <span class="highlight">
          <code>have-age-91</code><br>
          <span class="indent">:ARG1 entity<br> 
            :ARG2 age
          <span class="popup"><em>Ex:</em> The book I gave Martha was <strong>old</strong>.
    <strong>(h / have-age-91
        :ARG1</strong> (b / book
            :theme-of (g / give-01
                :actor (p / person
                    :refer-person 1st
                    :refer-number singular)
                :recipient (p2 / person :name (n / name :op1 "Martha"))
                :aspect performance
                :modal-strength full-affirmative))
        <strong>:ARG2 (o / old)</strong>
      </td>
      <td class="definition">The age of an entity.
        <span class="exsent">the <strong>3 year old</strong> boy
          <span class="popup">(b / boy
    <strong>:age (t / temporal-quantity
        :quant 3 
        :unit (y / year)</strong>)</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight"><code>:example</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          
      </td>
      <td>
        <span class="highlight"><code>:example-of</code>
          <span class="popup"><em>Ex:</em>
          
      </td>
      <td>
        <span class="highlight">
          <code>have-example-91</code><br>
          <span class="indent">:ARG1 event/entity<br> 
          :ARG2 example
      </td>
      <td class="definition">For exemplars.
        <span class="exsent">Countries <strong>like Germany and France</strong>. 
          <span class="popup">(c / country
    :refer-number plural
    <strong>:example (a / and
        :op1 (c2 / country 
            :name (n / name :op1 "Germany"))
        :op2 (c3 / country
            :name (n2 / name :op2 "France"))))</strong>)</span></span>
      </td>
    </tr>
    
    <tr>
      <td class="nowrap">
        <span class="highlight"><code>:ord</code></span><br><br>
        <span>child concept:</span><br>
        <span class="indent">
          <span class="highlight">(o / ordinal-entity)</span></span><br>
        <span>subroles:</span><br>
        <span class="indent">
          <span class="highlight">:value</span><br>
          <span class="highlight">:range</span><br>
          <span class="highlight">:range-start</span><br>
          <span class="highlight">:range-trajectory</span></span>
        <span class="popup"><em>Ex:</em> <strong></strong>
          popup
      </td>
      <td>
        <span class="highlight">
          <code>:ord-of</code>
          <span class="popup"><em>Ex:</em>
          
      </td>
      <td class="nowrap">
        <span class="highlight">
          <code>have-ord-91</code><br>
          <span class="indent">:ARG1 main entity<br> 
            :ARG2 ord<br> 
            :ARG3 range<br> 
            :ARG4 range-start<br>
            :ARG5 range-trajectory
      </td>
      <td class="definition">Ordinal relations. This role takes the concept <span class="highlight">ordinal-entity</span> as its value, with one mandatory subrole (<span class="highlight">:value</span>, for the number), and three optional subroles that give further information about how the counter is thinking about the counting.<br>
        <span class="exsent">the <strong>last</strong> man standing 
          <span class="popup">(m / man
    :actor-of (s / stand-01
        <strong>:ord (o / ordinal-entity :value "-1")</strong>
        :aspect state
        :modal-strength full-affirmative))</span></span>
        
        <span class="exsent">the <strong>first</strong> book <strong>in the stack</strong> 
          <span class="popup">(b / book
    <strong>:ord (o / ordinal-entity :value "1")</strong>
        :range (s / stack))</span></span>
            
        <span class="exsent">the <strong>3rd</strong> block <strong>from the lefthand side</strong> 
          <span class="popup">(b / block
    <strong>:ord (o / ordinal-entity :value "3")</strong>
        :range-start (s / side
            :ARG2-of (l / left-24)))</span></span>
            
        <span class="exsent">the <strong>2nd</strong> chair <strong>toward the front</strong>
          <span class="popup">(c / chair
    <strong>:ord (o / ordinal-entity :value "2")</strong>
        :range-trajectory (f / front-03))</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:list-item</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td class="nowrap">
        <span class="highlight">
          <code>:list-item-of</code>
          <span class="popup"><em>Ex:</em>
          </span>
        </span>
      </td>
      <td class="nowrap">
        <span class="highlight">
          <code>have-list-item-91</code><br>
          <span class="indent">:ARG1 entity<br> 
          :ARG2 number/value
      </td>
      <td class="definition">For enumeration of items in lists.
        <span class="exsent">I like two things: <strong>1.</strong> dogs, and <strong>2.</strong> coffee.
          <span class="popup">(l / like-01
    :experiencer (p / person
        :refer-person 1st
        :refer-number singular)
    :stimulus (t / thing
        :quant 2
        :ARG1-of (i / identity-91
            :ARG2 (a / and
                :op1 (d / dog
                    :refer-number plural
                    <strong>:list-item "1"</strong>)
                :op1 (c / coffee
                    <strong>:list-item "2"</strong>)))))</span></span>
      </td>
    </tr>
  </tbody>
</table>


<h2>Attribute Roles</h2>
<p>Attributes take their values from fixed sets of Constant Concepts.</p>

<table>
  <thead>
    <tr>
      <th>Role, Inverse, Reification</th>
      <th>Values</th>
      <th>Definitions</th>
    </tr>
  </thead>
  
  <tbody>
    <tr>
      <td rowspan="2" class="nowrap">
        <span class="highlight"><code>:polite</code></span><br><br>
        
        (no inverse)<br><br>
        
        <span class="highlight">
          <code>be-polite-91</code><br>
          <span class="indent">:ARG1 proposition<br> 
          :ARG2 politeness value
      </td>
      <td class="nowrap">
        <span class="highlight"><code>+</code>
      </td>
      <td class="definition">Politeness constructions.<br>
        <span class="exsent"><strong>Please</strong> pass the sugar. <br>
      </td>
    </tr>
    <tr>
      <td class="nowrap">
        <span class="highlight"><code>-</code>
      </td>
      <td class="definition">Rudeness constructions.<br>
        <span class="exsent"><strong></strong> <br>
      </td>
    </tr>
     
     
    <tr>
      <td rowspan="5">
        <span class="highlight"><code>:polarity</code></span><br><br>
        
        <span class="highlight"><code>:polarity-of</code></span><br><br>
        
        <span class="highlight"><code>have-polarity-91</code><br>
          <span class="indent">:ARG1 proposition<br> 
          :ARG2 polarity value
      </td>
      <td>
        <span class="highlight"><code>-</code>
      </td>
      <td class="definition">Simple negation.<br>
        <span class="exsent">We <strong>don't</strong> have money. <br>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>-intense</code>
      </td>
      <td class="definition">Double negation.<br>
        <span class="exsent">We <strong>ain't</strong> got <strong>no</strong> money.<br>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>+</code>
      </td>
      <td>Explicit affirmation.<br>
        <span class="exsent"><strong>Doch</strong>. 'yes it does so'<br>
      </td>
    </tr>
    <tr>
      <td class="nowrap">
        <span class="highlight"><code>(t / truth-value)</code>
      </td>
      <td class="definition">'Whether' constructions.<br>
        <span class="exsent">I don't know <strong>if</strong> I have money.<br>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>(u / umr-unknown)</code>
      </td>
      <td class="definition">Yes/no questions.<br>
        <span class="exsent"><strong>Do</strong> you have money?<br>
      </td>
    </tr>
    
     
    <tr>
      <td rowspan="3">
        <span class="highlight"><code>:mode</code></span><br><br>
        
        (no inverse)<br><br>
        
        (no reification)<br><br>
      </td>
      <td>
        <span class="highlight"><code>interrogative</code>
      </td>
      <td class="definition">Questions.<br>
        <span class="exsent"><strong>Who</strong> at the cheese? <br>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>imperative</code>
          <span class="popup"><em>Ex:</em>
      </td>
      <td class="definition">Commands, suggestions.<br>
        <span class="exsent"><strong>Move</strong> that block the other way.
          <span class="popup">(m / move-01 
        <strong>:mode imperative</strong>
        :actor (p / person
            :refer-person 2nd
            :refer-number singular)
        :theme (b / block
            :mod (t / that))
        :direction (w / way
                :mod-of (o / other-01))
        :aspect performance
        :modal-strength partial-affirmative</span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>expressive</code>
      </td>
      <td class="definition">Expressive constructions, profanity.
        <span class="exsent">I can't find my <strong>flippin</strong> socks.
          <span class="popup">(f / find-01 
    <strong>:mode expressive</strong>
    :polarity -
    :actor (p / person
        :refer-person 1st
        :refer-number singular)
    :theme (s / sock
        :refer-number plural
        :mod (f / flippin))
        :aspect state
        :modal-strength full-negative</span></span>
      </td>
    </tr>
    
    
    <tr>
      <td rowspan="4">
        <span class="highlight"><code>:degree</code></span><br><br>
        
        <span class="highlight"><code>:degree-of</code></span><br><br>
        
        <span class="highlight"><code>have-degree-91</code>
          <span class="indent">:ARG1 entity<br>
          :ARG2 attribute<br> 
          :ARG3 degree<br> 
          :ARG4 compared to<br> 
          :ARG5 reference to superset<br> 
          :ARG6 threshold of sufficiency</span></span><br><br>
          
        <span class="highlight"><code>have-degree-92</code>
          <span class="indent">:ARG1 state<br>
          :ARG2 degree value</span></span>
      </td>
      <td>
        <span class="highlight"><code>intensifier</code>
      </td>
      <td class="definition">Intensifiers.<br>
        <span class="exsent"><strong></strong>. <br>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>downtoner</code>
      </td>
      <td class="definition">Downtoners.<br>
        <span class="exsent"><strong></strong>. <br>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>equal</code>
      </td>
      <td class="definition">Equivalency.<br>
        <span class="exsent"><strong></strong>. <br>
      </td>
    </tr>
    <tr>
      <td>
        <code>(some concept)</code>
      </td>
      <td class="definition">For cases where you want to insert a lexical item from the sentence.<br>
        <span class="exsent"><strong></strong>. <br>
      </td>
    </tr>
    
    
    <tr>
      <td rowspan="7">
        <span class="highlight"><code>:refer-person</code></span><br><br>
      
        (no inverse)<br><br>
        
        (no reification)
      </td>
      <td>
        <span class="highlight"><code>non-1st</code>
      </td>
      <td class="definition">2nd and 3rd are clustered together</td>
    </tr>
    <tr>
      <td>
        <span class="highlight">
          <code>non-3rd</code>
      </td>
      <td class="definition">1st and 2nd are clustered together</td>
    </tr>
    <tr>
      <td>
        <span class="highlight">
          <code>1st</code>
      </td>
      <td class="definition">1st person.<br>
        <span class="exsent"><strong></strong>. <br>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight">
        <code>2nd</code>
      </td>
      <td class="definition">2nd person.<br>
        <span class="exsent"><strong></strong>. <br>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight">
          <code>3rd</code>
      </td>
      <td class="definition">third person.<br>
        <span class="exsent"><strong></strong>. <br>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight">
          <code>1st-inclusive</code>
      </td>
      <td class="definition">1st person, you & me.<br>
        <span class="exsent"><strong></strong>. <br>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight">
          <code>1st-exclusive</code>
      </td>
      <td class="definition">1st person, me without you.<br>
        <span class="exsent"><strong></strong>. <br>
      </td>
    </tr>
    
    
    <tr>
      <td rowspan="9">
        <span class="highlight"><code>:refer-number</code></span><br><br>
      
        (no inverse)<br><br>
        
        (no reification)
      <td>
        <span class="highlight"><code>singular</code>
      </td>
      <td class="definition">singular.<br>
        <span class="exsent"><strong></strong>. <br>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>nonsingular</code>
      </td>
      <td class="definition"></td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>paucal</code>
      </td>
      <td class="definition"></td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>plural</code>
      </td>
      <td class="definition">plural.<br>
        <span class="exsent"><strong></strong>. <br>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>dual</code>
      </td>
      <td class="definition"></td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>non-dual-paucal</code>
      </td>
      <td class="definition"></td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>greater-plural</code>
      </td>
      <td class="definition"></td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>trial</code>
      </td>
      <td class="definition"></td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>non-trial-paucal</code>
      </td>
      <td class="definition"></td>
    </tr>
    
    
    <tr>
      <td>
        <span class="highlight"><code>:refer-definiteness</code></span><br><br>
      
        (no inverse)<br><br>
        
        (no reification)
      </td>
      <td>
        <span class="highlight"><code>class</code>
      </td>
      <td class="definition">Use for generic pronouns. Other uses not explored yet.<br>
        <span class="exsent"><strong>One</strong> does not simply walk into Mordor.<br>
          <strong>You</strong> shouldn't judge a book by its cover.
      </td>
    </tr>
  </tbody>
</table>


<h2>Modal Attribute Roles</h2>

<table>
  <thead>
    <tr>
      <th>Role</th>
      <th>Inverse</th>
      <th>Reification</th>
      <th>Definition</th>
    </tr>
  </thead>
  
  <tbody>
    <tr>
      <td rowspan="7">
        <span class="highlight"><code>:modal-strength</code></span><br><br>
      
        (no inverse)<br><br>
        
        <span class="highlight"><code>have-modal-strength-91</code>
          <span class="indent">:ARG1 proposition<br>
          :ARG2 value
      </td>
      <td>
        <span class="highlight"><code>full-affirmative</code>
      </td>
      <td class="definition">Simple assertions and facts:<br>
          <span class="exsent">The dog barked last night.</span>
        Certainty;<br>
        Predictive future:<br>
          <span class="exsent">Mary <strong>will</strong> go to Santa Fe.</span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>partial-affirmative</code>
      </td>
      <td class="definition">Strong epistemic modals, adverbs and adjectives<br>
          <span class="exsent">Mary <strong>must have</strong> gone to Santa Fe.<br>
            The dog <strong>probably</strong> barked last night.</span>
        Strong imperatives;<br>
          <span class="exsent"><strong>Go</strong> to Santa Fe, Mary.</span>
        Strong deontic modals:<br>
          <span class="exsent">Mary <strong>must</strong> go to Santa Fe.</span>
        Intention (<em>intend, plan, decide</em>),<br>
        Obligation,<br>
          <span class="exsent">Mary <strong>needs to</strong> go to Santa Fe.</span>
        Purpose clauses:<br>
          <span class="exsent">Mary went to Santa Fe <strong>to buy a new dog</strong>.</span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>neutral-affirmative</code>
      </td>
      <td class="definition">Weak epistemic modals, adverbs, and adjectives:<br>
          <span class="exsent">The dog <strong>may have</strong> barked last night.</span>
        Ability:<br>
          <span class="exsent">Mary <strong>can</strong> drive a car.</span>
        Conditional phrases:<br>
          <span class="exsent"><strong>If the dog barks</strong>, Mary will buy earplugs.</span>
        Hopes and fears:
          <span class="exsent">I <strong>hope</strong> the dog doesn't bark.</span>
        Weak deontic modals including desire and permission:<br>
          <span class="exsent">Mary <strong>wants</strong> to go to Santa Fe.</span>
          <span class="exsent">Mary <strong>is allowed to</strong> to go to Santa Fe.</span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>neutral-negative</code>
      </td>
      <td class="definition">Combination of (some) neutral-affirmative lexical items with negation.<br>
        <span class="exsent">The dog <strong>may not have</strong> barked last night.<br>
          Mary <strong>doesn't want</strong> go to Santa Fe.<br>
          I <strong>don't hope</strong> the dog doesn't bark.<br>
          <strong>If the dog does'nt bark</strong>, Mary will buy earplugs.
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>partial-negative</code>
      </td>
      <td class="definition">Negative imperatives;<br>
        Combination of (some) partial-affirmative lexical items with negation.
        <span class="exsent">The dog <strong>probably didn't</strong> bark last night. <br>
          Mary <strong>shouldn't</strong> go to Santa Fe.<br>
          Mary is <strong>probably not</strong> going to Santa Fe.<br>
          <strong>Don't go</strong> to Santa Fe, Mary.<br>
          Mary went to Santa Fe <strong>to not get woken up in the night</strong>.
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>full-negative</code>
      </td>
      <td class="definition">Negation: <em>not, never, no</em>;<br>
        Counterfactuals
        <span class="exsent">The dog <strong>didn't</strong> bark last night. <br>
          Mary <strong>won't</strong> go to Santa Fe.
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>undefined</code>
      </td>
      <td class="definition">when the modal strength is not specified, not inferrable.<br>
        <span class="exsent">I wonder <strong>whether</strong> Mary went to Santa Fe. <br>
      </td>
    </tr>
    
    
    <tr>
      <td>
        <span class="highlight"><code>:modal-predicate</code></span><br><br>
      
        (no inverse)<br><br>
      
        (no reification)
      </td>
      <td>(variable of pred)</td>
      <td class="definition">Marks the complement of a modalizing predicate.
        <span class="exsent">The dog wants <strong>to go outside</strong>. 
      </td>
    </tr>
    
    
    <tr>
      <td>
        <span class="highlight"><code>:quote</code></span><br><br>
        
        (no inverse)<br><br>
        
        (no reification)
      </td>
      <td>(variable of pred)</td>
      <td class="definition">Marks the utterance argument of a communication/speech predicate.
        <span class="exsent">The dog said <strong>"arf arf, barkity bark bark"</strong>. 
      </td>
    </tr>
  </tbody>
</table>


<h2>Aspect Attribute Role</h2>

<table>
  <thead>
    <tr>
      <th>Role</th>
      <th>Inverse</th>
      <th>Reification</th>
      <th>Definition</th>
    </tr>
  </thead>
  
    <tr>
      <td rowspan="26">
        <span class="highlight"><code>:aspect</code></span><br><br>
        
        (no inverse)<br><br>
        
        <span class="highlight"><code>have-aspect-91</code>
          <span class="indent">:ARG1 event<br> 
          :ARG2 aspect value
      </td>
      <td>
        <span class="highlight"><code>habitual</code>
      </td>
      <td class="definition">Occurs/occurred usually or habitually.
        <span class="exsent">He bakes pies. 
          <span class="popup">(b / bake-01
    :actor (p / person
        :refer-person 3rd
        :refer-number singular)
    :undergoer (p2 / pie
        :refer-number plural)
    <strong>:aspect habitual</strong>
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>generic</code>
      </td>
      <td class="definition">The event is a hallmark characteristic of a class of entities.
        <span class="exsent">Platypuses lay eggs. 
          <span class="popup">(l / lay-01
    :actor (p / platypus
        :refer-number plural)
    :undergoer (e / egg
        :refer-number plural)
    <strong>:aspect generic</strong>
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>imperfective</code>
      </td>
      <td class="definition">Ambiguous between <span class="highlight">state</span> and <span class="highlight">atelic-process</span>.
        <span class="exsent"> 
          <span class="popup"></span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="indent">
          <span class="highlight"><code>state</code>
      </td>
      <td class="definition">Unspecified type of <span class="highlight">state</span>.
        <span class="exsent">My cat loves tuna. 
          <span class="popup">(l / love-01
    :actor (c / cat
        :possessor (p / person
            :refer-person 1st
            :refer-number singular))
    :undergoer (t / tuna)
    <strong>:aspect state</strong>
    :modal-strength full-affirmative)</span></span>
    
        <span class="exsent">I didn't go to the store. 
          <span class="popup">(g / go-02
    :polarity -
    :actor (p / person
            :refer-person 1st
            :refer-number singular)
    :goal (s / store)
    <strong>:aspect state</strong>
    :modal-strength full-negative)</span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="indent">
          <span class="indent">
            <span class="highlight"><code>reversible-state</code>
      </td>
      <td class="definition">Acquired <span class="highlight">state</span> that is not permanent.
        <span class="exsent">My cat is hungry.
          <span class="popup">(h / hunger-01
	  :ARG0 (c / cat
		    :refer-number singular
		    :possessor (p / person
			      :refer-person 1st
			      :refer-number singular)))
    <strong>:aspect reversible-state</strong>
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="indent">
          <span class="indent">
            <span class="highlight"><code>irreversible-state</code>
      </td>
      <td class="definition">Acquired <span class="highlight">state</span> that is permanent.
        <span class="exsent">The wine glass is shattered.
          <span class="popup">(s / shatter-01
	  :ARG1 (g / glass
		    :refer-number singular
		    :purpose (w / wine))
	  <strong>:aspect irreversible-state</strong>
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="indent">
          <span class="indent">
            <span class="highlight"><code>point-state</code>
      </td>
      <td class="definition"><span class="highlight">State</span> that is acquired and reversed at a single point in time.
        <span class="exsent">It is 2:30pm.
          <span class="popup">(h / have-temporal-91
    :ARG1 (n / now)
    :ARG2 (d / date-entity
		    :time 14:30)
	  <strong>:aspect point-state</strong>
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="indent">
          <span class="indent">
            <span class="highlight"><code>inherent-state</code>
      </td>
      <td class="definition"><span class="highlight">State</span> that is not acquired and permanent.
        <span class="exsent">My cat is black and white.
          <span class="popup">(h / have-mod-91
    :ARG1 (c / cat
	      :refer-number singular
		    :possessor (p / person
		        :refer-person 1st
		        :refer-number singular))
	  :ARG2 (a / and
		    :op1 (b / black)
		    :op2 (w / white)
	  <strong>:aspect inherent-state</strong>
    :modal-strength full-affirmative))</span></span>
      </td>
    </tr>
    <tr>
      <td><span class="highlight"><code>process</code>
      </td>
      <td class="definition">Unspecified type of eventuality.
        <span class="exsent">He was late because of the fire.
          <span class="popup">(l / late-02
    :theme (p2 / person
        :refer-person 3rd
        :refer-number singular)
    :cause (f / fire-05
        <strong>aspect process</strong>
        :modal-strength full-affirmative)
    :aspect performance
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="indent">
          <span class="highlight"><code>atelic-process</code>
      </td>
      <td class="definition"><span class="highlight">Process</span> that does not reach a result state.
        <span class="exsent">I heard about his travels.
          <span class="popup">(h / hear-01
	  :ARG0 (p / person
		    :ref-person 1st
		    :ref-number singular)
	  :ARG1 (t / travel-01
		    :ARG0 (p2 / person
			      :ref-person 3rd
			      :ref-number singular)
		    :aspect process
		    :modal-strength full-affirmative)
	  <strong>:aspect state</strong>
	  :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="indent">
          <span class="indent">
            <span class="highlight"><code>activity</code>
      </td>
      <td class="definition"><span class="highlight">Process</span> that does not end.
        <span class="exsent">He drove west.
          <span class="popup">(d / drive
    :actor (p / person
        :refer-person 3rd
        :refer-number singular)
    :direction (t / trajectory
        :direction-of (w / west-01))
    <strong>:aspect activity</strong>
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="indent">
          <span class="indent">
            <span class="indent">
              <span class="highlight"><code>directed-activity</code>
      </td>
      <td class="definition"><span class="highlight">Process</span>process that does not end and does progress linearly along a scale.
        <span class="exsent">The soup was cooling on the counter.
          <span class="popup">(c / cool-01
	  :theme (s / soup)
	  :place (c2 / counter)
	  <strong>:aspect directed-activity</strong>
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="indent">
          <span class="indent">
            <span class="indent">
              <span class="highlight"><code>undirected-activity</code>
      </td>
      <td class="definition"><span class="highlight">Process</span> that does not end and does not progress linearly along a scale.
        <span class="exsent">The cat was meowing outside the door.
          <span class="popup">(m / meow-01
	  :actor (c / cat
		    :refer-number singular)
	  :place (o / outside
		    :op1 (d / door))
	  <strong>:aspect undirected-activity</strong>
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="indent">
          <span class="indent">
            <span class="highlight"><code>iterative</code>
      </td>
      <td class="definition"><span class="highlight">Process</span> that occurs repetitively and ongoingly.
        <span class="exsent">He tapped his foot to the beat.
          <span class="popup">(t / tap-01
	  :actor (p / person
	      :refer-person 3rd
		    :refer-number singular)
	  :instrument (f / foot
	      :part-of p)
    :manner (r / rate-entity-91
        :ARG4 (b / beat))
    <strong>:aspect iterative</strong>
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="indent">
          <span class="highlight"><code>perfective</code>
      </td>
      <td class="definition"><span class="highlight">Process</span> that comes to an end.
        <span class="exsent">He stopped singing.
          <span class="popup">(s / sing-01
	  :actor (p / person
	      :refer-person 3rd
		    :refer-number singular)
    <strong>:aspect perfective</strong>
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="indent">
          <span class="indent">
            <span class="highlight"><code>endeavor</code>
      </td>
      <td class="definition"><span class="highlight">Process</span> that ends without reaching a result state.
        <span class="exsent">He hit the stick against the fence.  
          <span class="popup">(h / hit-01
	  :actor (p / person
	      :refer-person 3rd
		    :refer-number singular)
    :instrument (s / stick)
    :goal (f / fence)
    <strong>:aspect endeavor</strong>
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="indent">
          <span class="indent">
            <span class="indent">
              <span class="highlight"><code>semelfactive</code>
      </td>
      <td class="definition"><span class="highlight">Process</span> that ends without reaching a result state and happens at a single point in time.
        <span class="exsent">The cat blinked.
          <span class="popup">(b / blink-01
	  :actor (c / cat)
    <strong>:aspect semelfactive</strong>
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="indent">
          <span class="indent">
            <span class="indent">
              <span class="highlight"><code>undirected-endeavor</code>
      </td>
      <td class="definition"><span class="highlight">Process</span> that ends without reaching a result state and does not progress linearly along a scale.
        <span class="exsent">The cat meowed for two hours until I woke up.
          <span class="popup">(m / meow-01
	  :actor (c / cat)
	  :duration (t / temporal-quantity
		    :quant 2
		    :unit (h / hour))
    :temporal (u / until
		    :op1 (w / wake-01
			      :theme (p / person
				        :refer-person 1st
				        :refer-number singular)
			      :aspect performance
			      :modal-strength full-affirmative))
    <strong>:aspect undirected-endeavor</strong>
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="indent">
          <span class="indent">
            <span class="indent">
              <span class="highlight"><code>directed-endeavor</code>
      </td>
      <td class="definition"><span class="highlight">Process</span> that ends without reaching a result state and progresses linearly along a scale.
        <span class="exsent">The soup cooled for an hour before we ate it.
          <span class="popup">(c / cool-01
	  :theme (s / soup)
	  :duration (t / temporal-quantity
		    :quant 1
		    :unit (h / hour))
	  :temporal (b / before
		    :op1 (e / eat-01
			      :actor (p / person
				        :refer-person 1st
				        :refer-number plural)
			      :undergoer s
			      :aspect performance
			      :modal-strength full-affirmative))
    <strong>:aspect directed-activity</strong>
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="indent">
          <span class="indent">
            <span class="highlight"><code>performance</code>
      </td>
      <td class="definition"><span class="highlight">Process</span> that ends and reaches a result state.
        <span class="exsent">The soup cooled for an hour before we ate it.
          <span class="popup">(c / cool-01
	  :theme (s / soup)
	  :duration (t / temporal-quantity
		    :quant 1
		    :unit (h / hour))
	  :temporal (b / before
		    :op1 (e / eat-01
			      :actor (p / person
				        :refer-person 1st
				        :refer-number plural)
			      :undergoer s
			      <strong>:aspect performance</strong>
			      :modal-strength full-affirmative))
    :aspect directed-activity
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="indent">
          <span class="indent">
            <span class="indent">
              <span class="highlight"><code>inceptive</code>
      </td>
      <td class="definition">An <span class="highlight">activity</span> or <span class="highlight">state</span> starts.
        <span class="exsent">He started singing.
          <span class="popup">(s / sing-01
	  :actor (p / person
	      :refer-person 3rd
		    :refer-number singular)
    <strong>:aspect inceptive</strong>
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="indent">
          <span class="indent">
            <span class="indent">
              <span class="highlight"><code>incremental-accomplishment</code>
      </td>
      <td class="definition"><span class="highlight">Process</span> that ends and reaches a result state, and progresses linearly along a scale.
        <span class="exsent">I ate an apple pancake.
          <span class="popup">(e / eat-01
	  :actor (p / person
		    :refer-person 1st
		    :refer-number singular)
	  :undergoer (p2 / pancake
		    :refer-number singular
		    :mod (a / apple))
    <strong>:aspect incremental-accomplishment</strong>
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="indent">
          <span class="indent">
            <span class="indent">
              <span class="highlight"><code>nonincremental-accomplishment</code>
      </td>
      <td class="definition"><span class="highlight">Process</span> that ends and reaches a result state, and does not progress linearly along a scale.
        <span class="exsent">Harry repaired the computer.
          <span class="popup">(r / repair-01
	  :actor (p / person
		    :name (n / name :op1 "Harry"))
	  :undergoer (c / computer
		    :refer-number singular)
    <strong>:aspect nonincremental-accomplishment</strong>
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="indent">
          <span class="indent">
            <span class="indent">
              <span class="highlight"><code>directed-achievement</code>
      </td>
      <td class="definition"><span class="highlight">Process</span> that ends and reaches a result state within a single point in time, and progresses linearly along a scale.
        <span class="exsent">
          <span class="popup"></span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="indent">
          <span class="indent">
            <span class="indent">
              <span class="indent"> 
                <span class="highlight"><code>reversible-directed-achievement</code>
      </td>
      <td class="definition"><span class="highlight">Process</span> that ends and reaches a result state, which is not permanent, within a single point in time, and progresses linearly along a scale.
        <span class="exsent">The door opened.
          <span class="popup">(o / open-01
	  :theme (d / door
		    :refer-number singular)
    <strong>:aspect reversible-directed-achievement</strong>
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="indent">
          <span class="indent">
            <span class="indent">
              <span class="indent"> 
                <span class="highlight"><code>irreversible-directed-achievement</code>
      </td>
      <td class="definition"><span class="highlight">Process</span> that ends and reaches a result state, which is permanent, within a single point in time, and progresses linearly along a scale.
        <span class="exsent">The window shattered.
          <span class="popup">(s / shatter-01
	  :undergoer (w / window
		    :refer-number singular)
    <strong>:aspect irreversible-directed-achievement</strong>
    :modal-strength full-affirmative)</span></span>
      </td>
    </tr>
    
  </tbody>
</table>

</body>
</html>
