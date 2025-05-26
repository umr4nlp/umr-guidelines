<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>UMR Abstract Concepts</title>
  <style>
    body {
      font-family: sans-serif;
      font-size: 0.9em;
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
      font-family: monospace;
      font-size: inherit;
      line-height: 1.2;
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
      padding-left: 2em;
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
      line-height: 1.2;
    }
    .definition {
      white-space: normal;
      width: auto;
      line-height: 1.2;
    }
    .nowrap {
      white-space: nowrap;
    }.smallcaps {
      font-variant: small-caps;
    }
    .wrap-indent {
      display: block;
      margin-left: 2em;
      text-indent: -1em;
      font-family: monospace;
      font-size: inherit;
    }
  </style>
</head>
<body>
  
<h1>Abstract Concepts</h1>
<p>These are generic concepts that can be used as leaf nodes in a graph, serving various purposes.</p>

<h3>Basic concepts for pronouns and implicit arguments.</h3>
<table>
  <thead>
    <tr>
      <th>Concept</th>
      <th>Subroles</th>
      <th>Definition</th>
    </tr>
  </thead>
    <tr>
      <td>
        <span class="highlight"><code><strong>(p / person)</strong></code>
      </td>
      <td class="nowrap" rowspan="4">
        <span class="highlight"><code>:refer-person</code></span><br>
        <span class="highlight"><code>:refer-number</code></span><br>
        <span class="highlight"><code>:refer-definiteness</code></span><br>
      </td>
      <td class="definition" rowspan="4">Top-level Named Entity types can be used as head concepts for pronouns or other places where you need a simple implicit concept. The most common ones are listed here.
        <span class="exsent"><strong>The teacher</strong> ate an apple.
          <span class="popup">(e / eat-01
    :ARG0 <strong>(p / person
        :ARG0-of (t / teach-01))</strong>
    :ARG1 (a / apple)
    :aspect performance
    :modal-strength full-affirmative)</span></span><br>
          
        <span class="exsent"><strong>It</strong> tasted mealy.
          <span class="popup">(t / tast-02
    :ARG1 <strong>(t / thing
        :refer-person 3rd
        :refer-number singular)</strong>
    :ARG2 (m / mealy)
    :aspect state
    :modal-strength full-affirmative)</span></span><br>
          
        <span class="exsent">My dog came up to me. <strong>He</strong> said "rwawr".
          <span class="popup">(s / say-91
    :ARG0 <strong>(a / animal
        :refer-person 3rd
        :refer-number singular)</strong>
    :ARG1 (s / string-entity :value "rwawr"
        :quote s)
    :ARG2 <strong>(p / person)</strong>  *implicit argument, links to 'me'
    :aspect performance
    :modal-strength full-affirmative)</span></span><br>
          
        <span class="exsent"><strong>It</strong> has no bearing on our work force today .
          <span class="popup">(s30s / say-91
    :ARG0 (s30p / person)
    :ARG1 (s30b / bear-06 
        :polarity -
        :ARG1 <strong>(s30e / event
            :refer-person 3rd
            :refer-number singular)</strong>
        :ARG2 (s30f / force
            :ARG0-of (s30w / work-01)
            :possessor (s30p2 / person
                :refer-person 1st
                :refer-number plural))
        :temporal (s30t / today)
        :aspect state
        :quote s30s))</span></span><br>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code><strong>(t / thing)</strong></code>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code><strong>(a / animal)</strong></code>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code><strong>(e / event)</strong></code>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight"><code><strong>(p / place)</strong></code>
      </td>
      <td rowspan="3">
        <span class="highlight"><code>:refer-number</code></span><br>
      </td>
      <td class="definition" rowspan="3">Other common implicit concepts can come from the names of roles. Some common ones are listed.
        <span class="exsent"> Well it's another Sunday and I'm here <strong>at work</strong> again!
          <span class="popup">(s1a / and
    :op1 (s1h3 / have-temporal-91
        :ARG1 (s1n / now)
        :ARG2 (s1d / date-entity
            :weekday (s1s / sunday)
            :mod (s1a2 / another))
        :aspect state
        :modal-strength full-affirmative)
    :op2 (s1h2 / have-place-91
        :ARG1 (s1p / person
            :refer-person 1st
            :refer-number singular)
        :ARG2 (s1h / here
            <strong>:place (s1p2 / place
                :place-of (s1w2 / work-01
                    :ARG0 s1p)))</strong>
        :mod (s1a3 / again)
        :aspect state
        :modal-strength full-affirmative))</span></span><br>
    
        <span class="exsent"> <strong>Average maturity</strong> of the funds' investments lengthened by a day to 41 days, <strong>the longest</strong> since early August, according to Donoghue's.
          <span class="popup">(s4s2 / say-91
    :ARG0 (s4c / company :wiki - 
        :name (s4n / name :op1 "Donoghue's"))
    :ARG1 (s4l / lengthen-01
        :ARG1 <strong>(s4t4 / temporal
            :duration-of</strong> (s4m / mature-01
                :ARG1 (s4t3 / thing
                    :refer-number plural
                    :ARG2-of (s4i / invest-01
                        :ARG0 (s4f / fund)))
                :ARG1-of (s4a2 / average-01)
                :aspect process))
        :ARG2 (s4t / temporal-quantity :quant 1
            :unit (s4d / day))
        :ARG4 (s4t2 / temporal-quantity :quant 41
            :unit (s4d2 / day)
            :ARG1-of (s4h / have-degree-91
                :ARG2 (s4l2 / long-03
                    :ARG1 s4t2)
                :ARG3 (s4m2 / most)
                :ARG5 <strong>(s4t5 / temporal
                    :temporal</strong> (s4s / since
                        :op1 (s4e2 / early-01
                            :ARG2 (s4d4 / date-entity :month 8))))))
        :aspect performance)
    :aspect state)</span></span><br>
        
        <span class="exsent"> The total of 18 deaths from malignant mesothelioma, lung cancer and asbestosis was far higher <strong>than expected</strong>, the researchers said.
          <span class="popup">(s15s / say-01
    :ARG0 (s15p / person
        :ARG0-of (s15r / research-01))
    :ARG1 (s15h2 / have-degree-91
        :ARG1 (s15q / quantity :quant 18
            :ARG2-of (s15h3 / have-quant-91 
                :ARG1 (s15s2 / sum-of 
                    :op1 (s15d / die-01
                        :cause (s15d4 / disease :wiki "Mesothelioma" 
                            :name (s15n / name :op1 "malignant" :op2 "mesothelioma"))
                        :aspect performance)
                    :op2 (s15d5 / die-01
                        :cause (s15d2 / disease :wiki "Lung_cancer" 
                            :name (s15n2 / name :op1 "lung" :op2 "cancer"))
                        :aspect performance)
                    :op3 (s15d6 / die-01
                        :cause (s15d3 / disease :wiki "Asbestosis" 
                            :name (s15n3 / name :op1 "asbestosis"))
                        :aspect performance))))
        :ARG2 (s15h / high-02)
        :ARG3 (s15m / more
            :degree intensifier)
        :ARG4 <strong>(s15q2 / quantity
            :ARG1-of</strong> (s15e / expect-01
                :ARG0 s15p
                :aspect state))
        :aspect state
        :quote s15s)
    :aspect performance)</span></span><br>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code><strong>(t / temporal)</strong></code>
      </td>
    </tr>
    <tr>
      <td class="nowrap">
        <span class="highlight"><code><strong>(q / quantity)</strong></code>
      </td>
    </tr>
  </tbody>
</table>


<h3>UMR-labeled concepts for questions, options, and meta-labeling</h3>
<table>
  <thead>
    <tr>
      <th>Concept</th>
      <th>Subroles</th>
      <th>Definition</th>
    </tr>
  </thead>    
    <tr>
      <td>
        <span class="highlight"><code><strong>(u / umr-unknown)</strong></code>
      </td>
      <td rowspan="">
        <span class="highlight"></span>
      </td>
      <td class="definition" rowspan="">Concept takes the place of the unknown argument in WH questions.
        <span class="exsent"> 
          <span class="popup"></span></span><br>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight"><code><strong>(t / truth-value)</strong></code>
      </td>
      <td class="nowrap">
        <span class="highlight"><code>:polarity-of</code></span>
      </td>
      <td class="definition">Used for 'whether' or 'if' phrases when they are used to indicate that the truth value of a proposition is not known.
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight"><code><strong>(u / umr-choice)</strong></code>
      </td>
      <td class="nowrap">
        <span class="highlight"><code>:op1</code></span> ... <span class="highlight"><code>:opX</code></span>
      </td>
      <td class="definition">Used for 'whether' or 'if' phrases when they are used to indicate that the truth value of a proposition is not known.
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight"><code><strong>(u / umr-empty)</strong></code>
      </td>
      <td>
        <span class="highlight"><code></code></span>
      </td>
      <td class="definition">Used if there is no text in a sentence presented for annotation.
      </td>
    </tr>
    
    <tr>
      <td class="nowrap">
        <span class="highlight"><code><strong>(u / umr-unintelligible)</strong></code>
      </td>
      <td>
        <span class="highlight"><code></code></span>
      </td>
      <td class="definition">Used if there is no understandable text in a sentence, preventing annotation.
      </td>
    </tr>
  </tbody>
</table>
  
  

<h3>Entity types and other special concepts</h3>
<table>
  <thead>
    <tr>
      <th>Concept</th>
      <th>Subroles</th>
      <th>Definition</th>
    </tr>
  </thead>    
    <tr>
      <td rowspan="14">
        <span class="highlight"><code><strong>(d / date-entity)</strong></span></code>
      </td>
      <td>
        <span class="highlight"><code>:calendar</code></span>
      </td>
      <td class="definition">
        <span class="exsent"><strong>The academic year</strong>
          <span class="popup">(d / date-entity
    :calendar (y / year 
        :mod (a / academia)))</span></span>
      </td>
    </tr>    
    <tr>
      <td>
        <span class="highlight"><code>:century</code></span>
      </td>
      <td class="definition">
        <span class="exsent"><strong>The 18th century</strong>
          <span class="popup">(d / date-entity
    :century 18) </span></span>
      </td>
    </tr>  
    <tr>
      <td>
        <span class="highlight"><code>:day</code></span>
      </td>
      <td class="definition">
        <span class="exsent">June <strong>24th</strong>
          <span class="popup">(d / date-entity
    <strong>:day 24</strong>
    :month 6)</span></span>
      </td>
    </tr>  
    <tr>
      <td>
        <span class="highlight"><code>:dayperiod</code></span>
      </td>
      <td class="definition">
        <span class="exsent"><strong>The morning</strong>
          <span class="popup">(d / date-entity
    :dayperiod (m / morning)) </span></span>
      </td>
    </tr>  
    <tr>
      <td>
        <span class="highlight"><code>:decade</code></span>
      </td>
      <td class="definition">
        <span class="exsent"><strong>The 1950s</strong>
          <span class="popup">(d / date-entity
    :decade 1950)</span></span>
      </td>
    </tr>  
    <tr>
      <td>
        <span class="highlight"><code>:era</code></span>
      </td>
      <td class="definition">
        <span class="exsent">24th year of <strong>Heisei era</strong> 
          <span class="popup">(d / date-entity
   <strong>:era (h / heisei)</strong>
   :year 24)</span></span>
      </td>
    </tr>  
    <tr>
      <td>
        <span class="highlight"><code>:month</code></span>
      </td>
      <td class="definition">
        <span class="exsent"><strong>June</strong> 24th
          <span class="popup">(d / date-entity
    :day 24
    <strong>:month 6</strong>)</span></span>
      </td>
    </tr>  
    <tr>
      <td>
        <span class="highlight"><code>:quarter</code></span>
      </td>
      <td class="definition">
        <span class="exsent"><strong>4th quarter</strong>, 2011
          <span class="popup">(d / date-entity
    :year 2011
    <strong>:quarter 4</strong>)</span></span>
      </td>
    </tr>  
    <tr>
      <td>
        <span class="highlight"><code>:season</code></span>
      </td>
      <td class="definition">
        <span class="exsent"><strong>Winter</strong> 2011-2012
          <span class="popup">(d / date-entity
   :year 2011
   :year2 2012
   <strong>:season (w / winter)</strong>)</span></span>
      </td>
    </tr>  
    <tr>
      <td>
        <span class="highlight"><code>:time </code></span>
      </td>
      <td class="definition">
        <span class="exsent">4:30 pm
          <span class="popup">(d / date-entity
   :time "16:30")</span></span>
      </td>
    </tr>  
    <tr>
      <td>
        <span class="highlight"><code>:timezone</code></span>
      </td>
      <td class="definition">
        <span class="exsent">4:30 pm <strong>MDT</strong>
          <span class="popup">(d / date-entity
   :time "16:30"
   <strong>:timezone (m / MDT)</strong>)</span></span>
      </td>
    </tr>  
    <tr>
      <td>
        <span class="highlight"><code>:weekday</code></span>
      </td>
      <td class="definition">
        <span class="exsent">Thursday
          <span class="popup">(d / date-entity
    :weekday (t / thursday))</span></span>
      </td>
    </tr>  
    <tr>
      <td>
        <span class="highlight"><code>:year</code></span>
      </td>
      <td class="definition">
        <span class="exsent">4th quarter, <strong>2011</strong>
          <span class="popup">(d / date-entity
    <strong>:year 2011</strong>
    :quarter 4)</span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>:year2</code></span>
      </td>
      <td class="definition">
        <span class="exsent">Winter 2011-<strong>2012</strong>
          <span class="popup">(d / date-entity
   :year 2011
   <strong>:year2 2012</strong>
   :season (w / winter))</span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight"><code><strong>string-entity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:value</code></span>
      </td>
      <td class="definition">def
        <span class="exsent"> 
          <span class="popup"></span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight"><code><strong>ordinal-entity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:value</code></span><br>
        <span class="highlight"><code>:range</code></span><br>
        <span class="highlight"><code>:range-start</code></span><br>
        <span class="highlight"><code>:range-trajectory</code></span>
      </td>
      <td class="definition">def
        <span class="exsent"> 
          <span class="popup"></span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight"><code><strong>url-entity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:value</code></span>
      </td>
      <td class="definition">def
        <span class="exsent"> 
          <span class="popup"></span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight"><code><strong>percentage-entity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:value</code></span>
      </td>
      <td class="definition">def
        <span class="exsent"> 
          <span class="popup"></span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight"><code><strong>phone-number-entity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:value</code></span>
      </td>
      <td class="definition">def
        <span class="exsent"> 
          <span class="popup"></span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight"><code><strong>email-address-entity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:value</code></span>
      </td>
      <td class="definition">def
        <span class="exsent"> 
          <span class="popup"></span></span>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight"><code><strong>score-entity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:op1</code></span>... <span class="highlight"><code>:opX</code></span>
      </td>
      <td class="definition">def
        <span class="exsent"> 
          <span class="popup"></span></span>
      </td>
    </tr>
       
    <tr>
      <td>
        <span class="highlight"><code><strong>date-interval</strong></code>
      </td>
      <td rowspan="">
        <span class="highlight"><code>:op1</code></span><br>
        <span class="highlight"><code>:op2</code></span>
      </td>
      <td class="definition" rowspan="">
        <span class="exsent"> 
          <span class="popup"></span></span>
      </td>
    </tr>
       
    <tr>
      <td>
        <span class="highlight"><code><strong>value-interval</strong></code>
      </td>
      <td rowspan="">
        <span class="highlight"><code>:op1</code></span><br>
        <span class="highlight"><code>:op2</code></span>
      </td>
      <td class="definition" rowspan="">
        <span class="exsent"> 
          <span class="popup"></span></span>
      </td>
    </tr>
       
    <tr>
      <td>
        <span class="highlight"><code><strong>between</strong></code>
      </td>
      <td rowspan="">
        <span class="highlight"><code>:op1</code></span>... <span class="highlight"><code>:opX</code></span>
      </td>
      <td class="definition" rowspan="">
        <span class="exsent"> 
          <span class="popup"></span></span>
      </td>
    </tr>
       
    <tr>
      <td>
        <span class="highlight"><code><strong>slash</strong></code>
      </td>
      <td rowspan="">
        <span class="highlight"><code>:op1</code></span><br>
        <span class="highlight"><code>:op2</code></span>
      </td>
      <td class="definition">
        <span class="exsent"> 
          <span class="popup"></span></span>
      </td>
    </tr>
       
    <tr>
      <td>
        <span class="highlight"><code><strong>emoticon</strong></code>
      </td>
      <td rowspan="">
        <span class="highlight"><code>:value</code></span>
      </td>
      <td class="definition">
        <span class="exsent"> 
          <span class="popup"></span></span>
      </td>
    </tr>
       
    <tr>
      <td>
        <span class="highlight"><code><strong>relative-position</strong></code>
      </td>
      <td rowspan="">
        <span class="highlight"><code>:op1</code></span><br>
        <span class="highlight"><code>:quant</code></span><br>
        <span class="highlight"><code>:direction</code></span>
      </td>
      <td class="definition" rowspan="">
        <span class="exsent"> 
          <span class="popup"></span></span>
      </td>
    </tr>
       
    <tr>
      <td>
        <span class="highlight"><code><strong>relative-orientation</strong></code>
      </td>
      <td rowspan="">
        <span class="highlight"><code>:op1</code></span><br>
        <span class="highlight"><code>:quant</code></span><br>
        <span class="highlight"><code>:orientation</code></span>
      </td>
      <td class="definition" rowspan="">
        <span class="exsent"> 
          <span class="popup"></span></span>
      </td>
    </tr>
       
    <tr>
      <td>
        <span class="highlight"><code><strong>less-than</strong></code>
      </td>
      <td rowspan="">
        <span class="highlight"><code>:op1</code></span>
      </td>
      <td class="definition" rowspan="">
        <span class="exsent"> 
          <span class="popup"></span></span>
      </td>
    </tr>
       
    <tr>
      <td>
        <span class="highlight"><code><strong>more-than</strong></code>
      </td>
      <td rowspan="">
        <span class="highlight"><code>:op1</code></span>
      </td>
      <td class="definition" rowspan="">
        <span class="exsent"> 
          <span class="popup"></span></span>
      </td>
    </tr>
       
    <tr>
      <td>
        <span class="highlight"><code><strong>at-least</strong></code>
      </td>
      <td rowspan="">
        <span class="highlight"><code>:op1</code></span>
      </td>
      <td class="definition" rowspan="">
        <span class="exsent"> 
          <span class="popup"></span></span>
      </td>
    </tr>
       
    <tr>
      <td>
        <span class="highlight"><code><strong>at-most</strong></code>
      </td>
      <td rowspan="">
        <span class="highlight"><code>:op1</code></span>
      </td>
      <td class="definition" rowspan="">
        <span class="exsent"> 
          <span class="popup"></span></span>
      </td>
    </tr>
       
    <tr>
      <td>
        <span class="highlight"><code><strong>sum-of</strong></code>
      </td>
      <td rowspan="">
        <span class="highlight"><code>:op1</code></span>... <span class="highlight"><code>:opX</code></span>
      </td>
      <td class="definition" rowspan="">
        <span class="exsent"> 
          <span class="popup"></span></span>
      </td>
    </tr>
       
    <tr>
      <td>
        <span class="highlight"><code><strong>product-of</strong></code>
      </td>
      <td rowspan="">
        <span class="highlight"><code>:op1</code></span>... <span class="highlight"><code>:opX</code></span>
      </td>
      <td class="definition" rowspan="">
        <span class="exsent"> 
          <span class="popup"></span></span>
      </td>
    </tr>
       
    <tr>
      <td>
        <span class="highlight"><code><strong>ratio-of</strong></code>
      </td>
      <td rowspan="">
        <span class="highlight"><code>:op1</code></span>... <span class="highlight"><code>:opX</code></span>
      </td>
      <td class="definition" rowspan="">
        <span class="exsent"> 
          <span class="popup"></span></span>
      </td>
    </tr>
       
    <tr>
      <td>
        <span class="highlight"><code><strong>difference-of</strong></code>
      </td>
      <td rowspan="">
        <span class="highlight"><code>:op1</code></span>... <span class="highlight"><code>:opX</code></span>
      </td>
      <td class="definition" rowspan="">
        <span class="exsent"> 
          <span class="popup"></span></span>
      </td>
    </tr>
       
    <tr>
      <td>
        <span class="highlight"><code><strong>quotient-of</strong></code>
      </td>
      <td rowspan="">
        <span class="highlight"><code>:op1</code></span>... <span class="highlight"><code>:opX</code></span>
      </td>
      <td class="definition" rowspan="">
        <span class="exsent"> 
          <span class="popup"></span></span>
      </td>
    </tr>
       
    <tr>
      <td>
        <span class="highlight"><code><strong>power-of</strong></code>
      </td>
      <td rowspan="">
        <span class="highlight"><code>:op1</code></span><br>
        <span class="highlight"><code>:op2</code></span>
      </td>
      <td class="definition" rowspan="">
        <span class="exsent"> 
          <span class="popup"></span></span>
      </td>
    </tr>
       
    <tr>
      <td>
        <span class="highlight"><code><strong>root-of</strong></code>
      </td>
      <td rowspan="">
        <span class="highlight"><code>:op1</code></span><br>
        <span class="highlight"><code>:op2</code></span>
      </td>
      <td class="definition" rowspan="">
        <span class="exsent"> 
          <span class="popup"></span></span>
      </td>
    </tr>
       
    <tr>
      <td>
        <span class="highlight"><code><strong>logarithm-of</strong></code>
      </td>
      <td rowspan="">
        <span class="highlight"><code>:op1</code></span><br>
        <span class="highlight"><code>:op2</code></span>
      </td>
      <td class="definition" rowspan="">
        <span class="exsent"> 
          <span class="popup"></span></span>
      </td>
    </tr>
  </tbody>
</table>


<h3>Quantity Types</h3>
<table>
  <thead>
    <tr>
      <th>Concept</th>
      <th>Subroles</th>
      <th>Possible Values</th>
    </tr>
  </thead>  
    <tr>
      <td rowspan="2">
        <span class="highlight"><code><strong>monetary-quantity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:quant</code></span>
      </td>
      <td class="definition">def
        <span class="exsent">
          <span class="popup"></span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>:unit</code></span>
      </td>
      <td>
        <span class="highlight">dollar</span>, 
        <span class="highlight">euro</span>, 
        <span class="highlight">pound</span>, 
        <span class="highlight">yen</span>, 
        <span class="highlight">yuan</span>
      </td>
    </tr>
    
    <tr>
      <td rowspan="2">
        <span class="highlight"><code><strong>distance-quantity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:quant</code></span>
      </td>
      <td class="definition">def
        <span class="exsent">
          <span class="popup"></span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>:unit</code></span>
      </td>
      <td>
        <span class="highlight">meter</span>, 
        <span class="highlight">kilometer</span>, 
        <span class="highlight">inch</span>, 
        <span class="highlight">foot</span>, 
        <span class="highlight">yard</span>, 
        <span class="highlight">mile</span>, 
        <span class="highlight">light-year</span>, 
        <span class="highlight">kilo-base-pair</span>
      </td>
    </tr>
    
    <tr>
      <td rowspan="2">
        <span class="highlight"><code><strong>area-quantity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:quant</code></span>
      </td>
      <td class="definition">def
        <span class="exsent">
          <span class="popup"></span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>:unit</code></span>
      </td>
      <td>
        <span class="highlight">square-meter</span>, 
        <span class="highlight">square-kilometer</span>, 
        <span class="highlight">square-foot</span>, 
        <span class="highlight">acre</span>, 
        <span class="highlight">hectare</span>, 
        <span class="highlight">square-mile</span>
      </td>
    </tr>
    
    <tr>
      <td rowspan="2">
        <span class="highlight"><code><strong>volume-quantity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:quant</code></span>
      </td>
      <td class="definition">def
        <span class="exsent">
          <span class="popup"></span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>:unit</code></span>
      </td>
      <td>
        <span class="highlight">liter</span>, 
        <span class="highlight">cubic-meter</span>, 
        <span class="highlight">fluid-ounce</span>, 
        <span class="highlight">pint</span>, 
        <span class="highlight">gallon</span>, 
        <span class="highlight">cubic-mile</span>
      </td>
    </tr>
    
    <tr>
      <td rowspan="2">
        <span class="highlight"><code><strong>temporal-quantity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:quant</code></span>
      </td>
      <td class="definition">def
        <span class="exsent">
          <span class="popup"></span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>:unit</code></span>
      </td>
      <td>
        <span class="highlight">second</span>, 
        <span class="highlight">minute</span>, 
        <span class="highlight">hour</span>, 
        <span class="highlight">day</span>, 
        <span class="highlight">week</span>, 
        <span class="highlight">month</span>, 
        <span class="highlight">year</span>, 
        <span class="highlight">decade</span>, 
        <span class="highlight">century</span>
      </td>
    </tr>
    
    <tr>
      <td rowspan="2">
        <span class="highlight"><code><strong>frequency-quantity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:quant</code></span>
      </td>
      <td class="definition">def
        <span class="exsent">
          <span class="popup"></span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>:unit</code></span>
      </td>
      <td>
        <span class="highlight">hertz</span>
      </td>
    </tr>
    
    <tr>
      <td rowspan="2">
        <span class="highlight"><code><strong>speed-quantity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:quant</code></span>
      </td>
      <td class="definition">def
        <span class="exsent">
          <span class="popup"></span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>:unit</code></span>
      </td>
      <td>
        <span class="highlight">meter-per-second</span>, 
        <span class="highlight">mile-per-hour</span>
      </td>
    </tr>
    
    <tr>
      <td rowspan="2">
        <span class="highlight"><code><strong>acceleration-quantity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:quant</code></span>
      </td>
      <td class="definition">def
        <span class="exsent">
          <span class="popup"></span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>:unit</code></span>
      </td>
      <td>
        <span class="highlight">meter-per-second-squared</span>
      </td>
    </tr>
    
    <tr>
      <td rowspan="2">
        <span class="highlight"><code><strong>mass-quantity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:quant</code></span>
      </td>
      <td class="definition">def
        <span class="exsent">
          <span class="popup"></span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>:unit</code></span>
      </td>
      <td>
        <span class="highlight">kilogram</span>, 
        <span class="highlight">ounce</span>, 
        <span class="highlight">pound</span>,  
        <span class="highlight">ton</span>, 
        <span class="highlight">atomic-mass-unit</span>,  
        <span class="highlight">kilodalton</span> 
      </td>
    </tr>
    
    <tr>
      <td rowspan="2">
        <span class="highlight"><code><strong>force-quantity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:quant</code></span>
      </td>
      <td class="definition">def
        <span class="exsent">
          <span class="popup"></span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>:unit</code></span>
      </td>
      <td>
        <span class="highlight">newton</span>
      </td>
    </tr>
    
    <tr>
      <td rowspan="2">
        <span class="highlight"><code><strong>pressure-quantity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:quant</code></span>
      </td>
      <td class="definition">def
        <span class="exsent">
          <span class="popup"></span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>:unit</code></span>
      </td>
      <td>
        <span class="highlight">pascal</span>, 
        <span class="highlight">bar</span>, 
        <span class="highlight">psi</span>, 
        <span class="highlight">atmosphere</span>, 
        <span class="highlight">torr</span>
      </td>
    </tr>
    
    <tr>
      <td rowspan="2">
        <span class="highlight"><code><strong>energy-quantity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:quant</code></span>
      </td>
      <td class="definition">def
        <span class="exsent">
          <span class="popup"></span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>:unit</code></span>
      </td>
      <td>
        <span class="highlight">joule</span>, 
        <span class="highlight">calorie</span>, 
        <span class="highlight">kilowatt-hour</span>, 
        <span class="highlight">btu</span>, 
        <span class="highlight">electron-volt</span> 
      </td>
    </tr>
    
    <tr>
      <td rowspan="2">
        <span class="highlight"><code><strong>power-quantity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:quant</code></span>
      </td>
      <td class="definition">def
        <span class="exsent">
          <span class="popup"></span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>:unit</code></span>
      </td>
      <td>
        <span class="highlight">watt</span>, 
        <span class="highlight">horsepower</span>
      </td>
    </tr>
    
    <tr>
      <td rowspan="2">
        <span class="highlight"><code><strong>charge-quantity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:quant</code></span>
      </td>
      <td class="definition">def
        <span class="exsent">
          <span class="popup"></span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>:unit</code></span>
      </td>
      <td>
        <span class="highlight">coulomb</span>
      </td>
    </tr>
    
    <tr>
      <td rowspan="2">
        <span class="highlight"><code><strong>potential-quantity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:quant</code></span>
      </td>
      <td class="definition">def
        <span class="exsent">
          <span class="popup"></span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>:unit</code></span>
      </td>
      <td>
        <span class="highlight">volt</span>
      </td>
    </tr>
    
    <tr>
      <td rowspan="2">
        <span class="highlight"><code><strong>resistance-quantity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:quant</code></span>
      </td>
      <td class="definition">def
        <span class="exsent">
          <span class="popup"></span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>:unit</code></span>
      </td>
      <td>
        <span class="highlight">ohm</span>
      </td>
    </tr>
    
    <tr>
      <td rowspan="2">
        <span class="highlight"><code><strong>inductance-quantity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:quant</code></span>
      </td>
      <td class="definition">def
        <span class="exsent">
          <span class="popup"></span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>:unit</code></span>
      </td>
      <td>
        <span class="highlight">henry</span>
      </td>
    </tr>
    
    <tr>
      <td rowspan="2">
        <span class="highlight"><code><strong>magnetic-field-quantity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:quant</code></span>
      </td>
      <td class="definition">def
        <span class="exsent">
          <span class="popup"></span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>:unit</code></span>
      </td>
      <td>
        <span class="highlight">tesla</span>, 
        <span class="highlight">gauss</span>
      </td>
    </tr>
    
    <tr>
      <td rowspan="2">
        <span class="highlight"><code><strong>magnetic-flux-quantity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:quant</code></span>
      </td>
      <td class="definition">def
        <span class="exsent">
          <span class="popup"></span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>:unit</code></span>
      </td>
      <td>
        <span class="highlight">maxwell</span>, 
        <span class="highlight">weber</span>
      </td>
    </tr>
    
    <tr>
      <td rowspan="2">
        <span class="highlight"><code><strong>radiation-quantity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:quant</code></span>
      </td>
      <td class="definition">def
        <span class="exsent">
          <span class="popup"></span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>:unit</code></span>
      </td>
      <td>
        <span class="highlight">becquerel</span>, 
        <span class="highlight">curie</span>, 
        <span class="highlight">sievert</span>, 
        <span class="highlight">rem</span>, 
        <span class="highlight">gray</span>, 
        <span class="highlight">rad</span>
      </td>
    </tr>
    
    <tr>
      <td rowspan="2">
        <span class="highlight"><code><strong>fuel-consumption-quantity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:quant</code></span>
      </td>
      <td class="definition">def
        <span class="exsent">
          <span class="popup"></span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>:unit</code></span>
      </td>
      <td>
        <span class="highlight">liter-per-100-kilometer</span>, 
        <span class="highlight">mile-per-gallon</span>
      </td>
    </tr>
    
    <tr>
      <td rowspan="2">
        <span class="highlight"><code><strong>numerical-quantity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:quant</code></span>
      </td>
      <td class="definition">def
        <span class="exsent">
          <span class="popup"></span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>:unit</code></span>
      </td>
      <td>
        <span class="highlight">point</span>, 
        <span class="highlight">mole</span>
      </td>
    </tr>
    
    <tr>
      <td rowspan="2">
        <span class="highlight"><code><strong>information-quantity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:quant</code></span>
      </td>
      <td class="definition">def
        <span class="exsent">
          <span class="popup"></span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>:unit</code></span>
      </td>
      <td>
        <span class="highlight">bit</span>, 
        <span class="highlight">gigabit</span>, 
        <span class="highlight">byte</span>, 
        <span class="highlight">kilobyte</span>, 
        <span class="highlight">megabyte</span>, 
        <span class="highlight">gigabyte</span>, 
        <span class="highlight">terabyte</span>, 
        <span class="highlight">petabyte</span>, 
        <span class="highlight">exabyte</span>, 
        <span class="highlight">zettabyte</span>, 
        <span class="highlight">yottabyte</span>, 
        <span class="highlight">nibble</span>
      </td>
    </tr>
    
    <tr>
      <td rowspan="2">
        <span class="highlight"><code><strong>concentration-quantity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:quant</code></span>
      </td>
      <td class="definition">def
        <span class="exsent">
          <span class="popup"></span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>:unit</code></span>
      </td>
      <td>
        <span class="highlight">molar </span>, 
        <span class="highlight">micromolar </span>, 
        <span class="highlight">kilogram-per-cubit-meter</span>, 
        <span class="highlight">parts-per-million</span>, 
        <span class="highlight">katal </span>, 
        <span class="highlight">microkatal</span>, 
        <span class="highlight">nanokatal</span>, 
        <span class="highlight">enzyme-unit </span>
      </td>
    </tr>
    
    <tr>
      <td rowspan="2">
        <span class="highlight"><code><strong>catalytic-activity-quantity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:quant</code></span>
      </td>
      <td class="definition">def
        <span class="exsent">
          <span class="popup"></span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>:unit</code></span>
      </td>
      <td>
        <span class="highlight">katal </span>, 
        <span class="highlight">microkatal</span>, 
        <span class="highlight">nanokatal</span>, 
        <span class="highlight">enzyme-unit </span>
      </td>
    </tr>
    
    <tr>
      <td rowspan="2">
        <span class="highlight"><code><strong>acidity-quantity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:quant</code></span>
      </td>
      <td class="definition">def
        <span class="exsent">
          <span class="popup"></span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>:scale</code></span>
      </td>
      <td>
        <span class="highlight">ph</span>
      </td>
    </tr>
    
    <tr>
      <td rowspan="2">
        <span class="highlight"><code><strong>seismic-quantity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:quant</code></span>
      </td>
      <td class="definition">def
        <span class="exsent">
          <span class="popup"></span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>:scale</code></span>
      </td>
      <td>
        <span class="highlight">richter</span>
      </td>
    </tr>
    
    <tr>
      <td rowspan="3">
        <span class="highlight"><code><strong>temperature-quantity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:quant</code></span>
      </td>
      <td class="definition">def
        <span class="exsent">
          <span class="popup"></span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>:unit</code></span>
      </td>
      <td>
        <span class="highlight">degree</span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>:scale </code></span>
      </td>
      <td>
        <span class="highlight">celsius</span>, 
        <span class="highlight">kelvin</span>, 
        <span class="highlight">farenheit</span>, 
      </td>
    </tr>
    
    <tr>
      <td rowspan="2">
        <span class="highlight"><code><strong>seismic-quantity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:quant</code></span>
      </td>
      <td class="definition">def
        <span class="exsent">
          <span class="popup"></span></span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight"><code>:scale</code></span>
      </td>
      <td>
        <span class="highlight">degree</span>, 
        <span class="highlight">radian</span>
      </td>
    </tr>
  </tbody>
</table>


<h3>Spatial Concepts</h3>
<table>
  <thead>
    <tr>
      <th>Concept</th>
      <th>Subroles</th>
      <th>Definition</th>
    </tr>
  </thead>  
    <tr>
      <td>
        <span class="highlight"><code><strong>cartesian-coordinate-entity</strong></code>
      </td>
      <td rowspan="">
        <span class="highlight"><code>:x</code></span><br>
        <span class="highlight"><code>:y</code></span><br>
        <span class="highlight"><code>:z</code></span><br>
        <span class="highlight"><code>:framework</code></span>
      </td>
      <td class="definition" rowspan="">
        <span class="exsent"> 
          <span class="popup"></span></span><br>
      </td>
    </tr>  
    
    <tr>
      <td>
        <span class="highlight"><code><strong>dimension-entity</strong></code>
      </td>
      <td rowspan="">
        <span class="highlight"><code>:value</code></span><br>
        <span class="highlight"><code>:unit</code></span>
      </td>
      <td class="definition" rowspan="">
        <span class="exsent"> 
          <span class="popup"></span></span><br>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight"><code><strong>slope-quantity</strong></code>
      </td>
      <td>
        <span class="highlight"><code>:quant</code></span><br>
        <span class="highlight"><code>:rise-axis</code></span><br>
        <span class="highlight"><code>:run-axis</code></span>
      </td>
      <td class="definition">
        <span class="exsent"> 
          <span class="popup"></span></span><br>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight"><code><strong>composite-entity</strong></code>
      </td>
      <td>-</td>
      <td class="definition">def
        <span class="exsent"> 
          <span class="popup"></span></span><br>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight"><code><strong>space</strong></code>
      </td>
      <td>-</td>
      <td class="definition">def
        <span class="exsent"> 
          <span class="popup"></span></span><br>
      </td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight"><code><strong>trajectory</strong></code>
      </td>
      <td>-</td>
      <td class="definition">def
        <span class="exsent"> 
          <span class="popup"></span></span><br>
      </td>
    </tr>
  </tbody>
</table>

</body>
</html>
