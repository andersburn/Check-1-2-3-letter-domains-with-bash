

<h1>Domain Availability Checker Script</h1>

<p>This Bash script checks whether domains are available or taken by using the <code>whois</code> command. It works with any domain ending such as <b>.net</b>, <b>.ai</b>, <b>.io</b>, <b>.com</b>, <b>.dk</b>, and others. The script generates combinations of letters and numbers within a configurable length range and queries WHOIS servers directly to find out if the domains exist.</p>

<h2>Features</h2>
<ul>
  <li>Works with any top-level domain (e.g. .net, .ai, .io, .com, .dk).</li>
  <li>Customizable minimum and maximum length for domain names.</li>
  <li>Adjustable delay between lookups (<code>SLEEP_TIME</code>).</li>
  <li>Uses lowercase letters (a–z) and digits (0–9) for combinations.</li>
  <li>Automatically saves available and taken domains to separate files.</li>
  <li>Uses recursive generation to handle any length range without editing loops.</li>
</ul>

<h2>How It Works</h2>
<ol>
  <li>The script builds all possible combinations of letters and numbers within the chosen range.</li>
  <li>Each domain is checked with a WHOIS query, for example:
    <pre><code>whois example.net</code></pre>
  </li>
  <li>If the WHOIS result contains text such as <code>No match for</code> or <code>No entries found</code>, it is considered free. Otherwise, it is marked as taken.</li>
  <li>Free domains are saved in <code>free_domains_[MIN]-[MAX]char.txt</code> and taken ones in <code>taken_domains_[MIN]-[MAX]char.txt</code>.</li>
  <li>The script pauses between requests to respect WHOIS rate limits.</li>
</ol>

<h2>Configuration</h2>
<p>You can edit the first lines of the script to adjust its behavior:</p>

<pre><code>DOMAIN_ENDING=".net"    # Domain ending (.net, .ai, .io, .com, etc.)
SLEEP_TIME=1            # Seconds to wait between WHOIS lookups
MIN_LENGTH=1            # Minimum length of domain names
MAX_LENGTH=3            # Maximum length of domain names
</code></pre>

<p>Example configurations:</p>

<ul>
  <li><b>1–3 character .net domains:</b><br>
  <code>DOMAIN_ENDING=".net"</code><br>
  <code>MIN_LENGTH=1</code><br>
  <code>MAX_LENGTH=3</code></li>
  <li><b>Only 2-character .ai domains:</b><br>
  <code>DOMAIN_ENDING=".ai"</code><br>
  <code>MIN_LENGTH=2</code><br>
  <code>MAX_LENGTH=2</code></li>
  <li><b>4–5 character .com domains with 2 seconds delay:</b><br>
  <code>DOMAIN_ENDING=".com"</code><br>
  <code>SLEEP_TIME=2</code><br>
  <code>MIN_LENGTH=4</code><br>
  <code>MAX_LENGTH=5</code></li>
</ul>
<h3>Errors?</h3>
<p>if it dosen't work:</p>
<ul>
<li>Try to change sleeptime</li>
<li>add a new "Domain not found" line to the script. Check a domain that is not taken with "whois longdomainthatnoonewants.yourending" and see how it says: Domain not found, add this to the list of "Domain not found"-types</li>

<h2>How to Run</h2>
<ol>
  <li>Copy the script into a file, for example <code>check_domains.sh</code>.</li>
  <li>Make it executable:
    <pre><code>chmod +x check_domains.sh</code></pre>
  </li>
  <li>Run it in your terminal:
    <pre><code>./check_domains.sh</code></pre>
  </li>
  <li>Watch the output for lines like:
    <pre><code>[FREE]  ab.net
[TAKEN] ac.net</code></pre>
  </li>
  <li>When done, open the generated files to see results:
    <ul>
      <li><code>free_domains_[MIN]-[MAX]char.txt</code></li>
      <li><code>taken_domains_[MIN]-[MAX]char.txt</code></li>
    </ul>
  </li>
</ol>

<h2>Notes</h2>
<ul>
  <li>Different WHOIS servers return different messages for free domains. If needed, adjust the search phrase in the script to match the response for the chosen TLD.</li>
  <li>To avoid being blocked, do not reduce the sleep time too much. 1 second per query is generally safe.</li>
  <li>Scanning large ranges (e.g., 3–5 characters) can take a very long time.</li>
</ul>

