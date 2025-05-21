<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>UMR Relations and Rolesets</title>
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
    }
    th {
      background-color: #f0f0f0;
    }
    .highlight {
      background-color: #e6f2ff;
      border-radius: 4px;
      padding: 0.1em 0.3em;
      display: inline-block;
      position: relative;
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
      white-space: pre;
      font-family: monospace;
    }
    .highlight:hover .popup {
      display: block;
    }
  </style>
</head>
<body>

<h1>UMR Relations & Rolesets</h1>

<p>This is a reference page with lists of UMR participant roles, non-participant roles, and attribute roles, along with their inverse forms and reifications. Examples are given in English with English PropBank roleset labels (for sense disambiguation), but without the numbered args associated with the rolesets. </p>

<h2>Participant Roles</h2>
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
          <code>:actor</code>
          <span class="popup"><em>Ex:</em> <strong>He</strong> ate the corn.
    (e / eat-01
        <strong>:actor (p / person
            :refer-person 3rd
            :refer-number singular)</strong>
        :undergoer (c / corn)
        :aspect performance
        :modal-strength full-affirmative)
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>:actor-of</code>
          <span class="popup"><em>Ex:</em> I saw <strong>the boy</strong> who ate the corn.
    (s / see-01
        :experiencer (p / person
            :refer-person 1st
            :refer-number singular)
        :stimulus <strong>(b / boy
            :actor-of</strong> (e / eat-01
                :undergoer (c / corn)
                :aspect performance
                :modal-strength full-affirmative))
        :aspect state
        :modal-strength full-affirmative)
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>have-actor-91</code>
      </td>
      <td>animate entity that initiates the action</td>
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
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>:co-actor-of</code>
          <span class="popup"><em>Ex:</em> They fired <strong>the man</strong> I was arguing with.
    (f / fire-02
        :actor (p / person
            :refer-person 3rd
            :refer-number plural)
        :undergoer <strong>(m / man
            :co-actor-of</strong> (a / argue-01
                :actor (p2 / person
                   :refer-person 1st
                   :refer-number singular)
               :aspect activity
               :modal-strength full-affirmative))
       :aspect performance
       :modal-strength full-affirmative)
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>have-co-actor-91</code>
      </td>
      <td>secondary parallel actor who is acting independently of the primary :actor</td>
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
        :modal-strength full-affirmative)</span></span></td>
          <td><span class="highlight"><code>:undergoer-of</code><span class="popup"><em>Ex:</em> I grew <strong>the corn</strong>the boy ate.<br>(g / grow-01
        :actor (p / person
            :refer-person 1st
            :refer-number singular)
        :undergoer <strong>(c / corn
           :undergoer-of</strong> (e / eat-01
                :actor (b / boy)
                :aspect performance
               :modal-strength full-affirmative))
        :aspect performance
        :modal-strength full-affirmative)
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>have-undergoer-91</code>
      </td>
      <td>entity (animate or inanimate) that is affected by the action</td>
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
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>:theme-of</code>
          <span class="popup"><em>Ex:</em> I dusted <strong>the books</strong> she had put on the shelf.
    (d / dust-01
        :actor (p / person
            :refer-person 1st
            :refer-number singular)
        <strong:source (b / book
            :refer-number plural
            :theme-of></strong> (p2 / put-01
                :actor (p3 / person
                    :refer-person 3rd
                    :refer-number singular)
                :goal (s / shelf)
                :aspect performance
                :modal-strength full-affirmative))
        :aspect performance
        :modal-strength full-affirmative)
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>have-theme-91</code>
      </td>
      <td>entity (animate, inanimate, or abstract) that moves from one entity to another entity, either spatially or metaphorically</td>
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
          </span>
        </span>
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
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>have-recipient-91</code></td>
      <td>animate entity that gains possession (or at least temporary control) of another entity</td>
    </tr>
    <tr>
      <td><span class="highlight"><code>:force</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>:force-of</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>have-force-91</code></td>
      <td>inanimate entity that initiates the action</td>
    </tr>
    <tr>
      <td><span class="highlight"><code>:causer</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>:causer-of</code><span class="popup"><em>Ex:</em> <strong></strong><br>
      </span></span></td></td>
      <td><span class="highlight"><code>have-causer-91</code></td>
      <td>animate entity that acts on another animate entity to initiate the action</td>
    </tr>
    <tr>
      <td><span class="highlight"><code>:experiencer</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>:experiencer-of</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>have-experience-91</code></td>
      <td>animate entity that cognitively or sensorily experiences a stimulus</td>
    </tr>
    <tr>
      <td><span class="highlight"><code>:stimulus</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>:stimulus-of</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>have-experience-91</code></td>
      <td>entity (animate or inanimate) that is experienced by an experiencer</td>
    </tr>
    <tr>
      <td><span class="highlight"><code>:instrument</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>:instrument-of</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span <span class="highlight"><code>have-instrument-91</code></td>
      <td>inanimate entity that is manipulated by an external causer in order to initiate the action</td>
    </tr>
    <tr>
      <td><span class="highlight"><code>:companion</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>:companion-of</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>have-companion-91</code></td>
      <td>animate entity that acts with the actor to initiate the action</td>
    </tr>
    <tr>
      <td><span class="highlight"><code>:material</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>:material-of</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>have-material-91</code></td>
      <td>entity (inanimate) that is transformed into a new entity</td>
    </tr>
    <tr>
      <td><span class="highlight"><code>:source</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>:source-of</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>have-source-91</code></td>
      <td>entity from which the theme detaches</td>
    </tr>
    <tr>
      <td><span class="highlight"><code>:place</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>:place-of</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>have-place-91</code></td>
      <td>location at which the action takes place</td>
    </tr>
    <tr>
      <td><span class="highlight"><code>:start</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>:start-of</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>have-start-91</code></td>
      <td>location at which a motion event begins</td>
    </tr>
    <tr>
      <td><span class="highlight"><code>:goal</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>:goal-of</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>have-goal-91</code></td>
      <td>location at which the action ends, the end point at which the theme arrives</td>
    </tr>
    <tr>
      <td><span class="highlight"><code>:affectee</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>:affectee-of</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>have-affectee-91</code></td>
      <td>animate entity which the action has a positive or negative influence on, i.e. beneficiary or maleficiary</td>
    </tr>
    <tr>
      <td><span class="highlight"><code>:cause</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>:cause-of</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>have-cause-91</code></td>
      <td>inanimate entity that causes the action to happen</td>
    </tr>
    <tr>
      <td><span class="highlight"><code>:manner</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>:manner-of</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>have-manner-91</code></td>
      <td>manner in which the action takes place</td>
    </tr>
    <tr>
      <td><span class="highlight"><code>:reason</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>:reason-of</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>have-reason-91</code></td>
      <td>motivation for the actor to initiate the action</td>
    </tr>
    <tr>
      <td><span class="highlight"><code>:purpose</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>:purpose-of</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>have-purpose-91</code></td>
      <td>intended event that results from the action</td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:result</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>:result-of</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>have-result-91</code></td>
      <td>event or state that comes about in some way that is contingent on another event</td>
    </tr>
    
    <tr>
      <td><span class="highlight"><code>:temporal</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>:temporal-of</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>have-temporal-91</code></td>
      <td>element that has a temporal relation with the action</td>
    </tr>
    
    <tr>
      <td><span class="highlight"><code>:extent</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>:extent-of</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>have-extent-91</code></td>
      <td>measurement phrase</td>
    </tr>
    
    <tr>
      <td><span class="highlight"><code>:other-role</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>:other-role-of</code><span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight"><code>have-other-role-91</code></td>
      <td>this role can be used when an annotator is unsure of which role is appropriate</td>
    </tr>
  </tbody>
</table>

<h2>Non-Participant Roles</h2>
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
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>:direction-of</code>
          <span class="popup"><em>Ex:</em>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>have-direction-91</code>
      </td>
      <td>direction of motion</td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:path</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>:path-of</code>
          <span class="popup"><em>Ex:</em>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>have-path-91</code>
      </td>
      <td></td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:quant</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>:quant-of</code>
          <span class="popup"><em>Ex:</em>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>have-quant-91</code>
      </td>
      <td></td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:duration</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>:duration-of</code>
          <span class="popup"><em>Ex:</em>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>have-duration-91</code>
      </td>
      <td></td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:frequency</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>:frequency-of</code>
          <span class="popup"><em>Ex:</em>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>have-frequency-91</code>
      </td>
      <td></td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:mod</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>:mod-of</code>
          <span class="popup"><em>Ex:</em>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>have-mod-91</code>
      </td>
      <td></td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:topic</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>:topic-of</code>
          <span class="popup"><em>Ex:</em>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>have-topic-91</code>
      </td>
      <td></td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:vocative</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>:vocative-of</code>
          <span class="popup"><em>Ex:</em>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>have-vocative-91</code>
      </td>
      <td></td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:medium</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>:medium-of</code>
          <span class="popup"><em>Ex:</em>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>have-medium-91</code>
      </td>
      <td></td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:possessor</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>:possessor-of</code>
          <span class="popup"><em>Ex:</em>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>have-poss-91</code>
      </td>
      <td></td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:part</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>:part-of</code>
          <span class="popup"><em>Ex:</em>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>have-part-91</code>
      </td>
      <td></td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:group</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>:group-of</code>
          <span class="popup"><em>Ex:</em>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>have-group-91</code>
      </td>
      <td></td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:age</code>
          <span class="popup"><em>Ex:</em> <strong></strong>.
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>:age-of</code>
          <span class="popup"><em>Ex:</em>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>have-age-91</code>
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
          </span>
      </td>
      <td></td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:example</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>:example-of</code>
          <span class="popup"><em>Ex:</em>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>have-example-91</code>
      </td>
      <td></td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:ord</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>:ord-of</code>
          <span class="popup"><em>Ex:</em>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>have-ord-91</code>
      </td>
      <td></td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:list-item</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>:list-item-of</code>
          <span class="popup"><em>Ex:</em>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>have-list-item-91</code>
      </td>
      <td></td>
    </tr>
  </tbody>
</table>


<h2>Attribute Roles</h2>
<table>
  <thead>
    <tr>
      <th>Role</th>
      <th>Values/Reification</th>
      <th>Definition</th>
    </tr>
  </thead>
  <tbody>  
    <tr>
      <td rowspan="3">
        <span class="highlight">
          <code>:polite</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td>
        <span class="highlight">
          <code>be-polite-91</code>
        </span>
      </td>
      <td>definition</td>
    </tr>
    <tr>
      <td>
        <span class="highlight">
          <code>+</code>
        </span>
      </td>
    </tr>
    <tr>
      <td>
        <span class="highlight">
          <code>-</code>
        </span>
      </td>
    </tr>
    <tr></tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:polarity</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td></td>
      <td>
        <span class="highlight">
          <code>have-polarity-91</code>
      </td>
      <td></td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:mode</code>
          <span class="popup"><em>Ex:</em><strong>Imperative:</strong> Move that block the other way.
    (m / move-01 
        <strong>:mode imperative</strong>
        :actor (p / person
            :refer-person 2nd
            :refer-number singular)
        :theme (b / block
            :mod (t / that))
        :direction (w / way
                :mod-of (o / other-01))
        :aspect performance
        :modal-strength partial-affirmative)
        
        <em>Ex:</em><strong>Expressive:</strong> .
        
        <em>Ex:</em><strong>Interrogative:</strong> .
          </span>
        </span>
      </td>
      <td></td>
      <td>
        <code>-</code>
      </td>
      <td></td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:degree</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td></td>
      <td>
        <span class="highlight">
          <code>have-degree-91, have-degree-92</code>
      </td>
      <td></td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:refer-person</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td></td>
      <td>
        <code>-</code>
      </td>
      <td></td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:refer-number</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td></td>
      <td>
        <code>-</code>
      </td>
      <td></td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:modal-strength</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td></td>
      <td>
        <span class="highlight">
          <code>have-modal-strength-91</code>
      </td>
      <td></td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:modal-predicate</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td></td>
      </td>
        <code>-</code>
      </td>
      <td></td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:quote</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td></td>
      </td>
        <code>-</code>
      </td>
      <td></td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:aspect</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td></td>
      <td>
        <span class="highlight">
          <code>have-aspect-91</code>
      </td>
      <td></td>
    </tr>
    
    <tr>
      <td>
        <span class="highlight">
          <code>:aspect</code>
          <span class="popup"><em>Ex:</em> <strong></strong>
          </span>
        </span>
      </td>
      <td></td>
      <td>
        <span class="highlight">
          <code>have-aspect-91</code>
      </td>
      <td></td>
    </tr>
  </tbody>
</table>

</body>
</html>
