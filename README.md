# job-board--
<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Job Board</title>
<style>
 body{font-family:Arial, sans-serif; margin:0; background:#f5f7fb;}
 header{background:#1a73e8; color:white; padding:16px; font-size:22px; font-weight:600;}
 .container{padding:20px; max-width:900px; margin:auto;}
 .search-area{display:flex; gap:10px;}
 input, select{padding:10px; font-size:15px; flex:1; border-radius:6px; border:1px solid #ccc;}
 button{padding:10px 18px; background:#1a73e8; color:white; border:0; border-radius:6px; cursor:pointer;}
 button:hover{opacity:0.9;}
 .job-card{background:white; padding:16px; border-radius:8px; margin-top:16px; box-shadow:0 2px 6px rgba(0,0,0,0.1);} 
 .job-title{font-size:18px; font-weight:600;}
 .job-company{color:#444; margin:6px 0;}
 .job-tag{display:inline-block; margin-right:6px; background:#e8f0fe; padding:5px 10px; border-radius:5px; font-size:13px;}
 .apply-btn{margin-top:10px; display:inline-block; background:#34a853; color:white; padding:8px 14px; border-radius:6px; text-decoration:none;}
</style>
</head>
<body>
<header>Job Board</header>
<div class="container">
  <div class="search-area">
    <input type="text" id="searchText" placeholder="Search job title..." />
    <select id="filterLoc">
      <option value="">Location</option>
      <option>Remote</option>
      <option>India</option>
      <option>USA</option>
      <option>UK</option>
    </select>
    <button onclick="searchJobs()">Search</button>
  </div>

  <div id="jobList"></div>
</div>

<script>
const jobs = [
  {title:"Frontend Developer", company:"Google", loc:"Remote", tags:["React","JavaScript"], link:"#"},
  {title:"Backend Developer", company:"Amazon", loc:"India", tags:["Java","Spring"], link:"#"},
  {title:"AI Engineer", company:"OpenAI", loc:"USA", tags:["Python","ML"], link:"#"},
  {title:"Data Analyst", company:"TCS", loc:"India", tags:["SQL","Excel"], link:"#"}
];

function renderJobs(list){
  const c = document.getElementById('jobList');
  c.innerHTML = '';
  list.forEach(j => {
    c.innerHTML += `
      <div class="job-card">
        <div class="job-title">${j.title}</div>
        <div class="job-company">${j.company} • ${j.loc}</div>
        <div>${j.tags.map(t=>`<span class='job-tag'>${t}</span>`).join('')}</div>
        <a class="apply-btn" href="${j.link}">Apply</a>
      </div>`;
  });
}

function searchJobs(){
  let txt = document.getElementById('searchText').value.toLowerCase();
  let loc = document.getElementById('filterLoc').value;
  let filtered = jobs.filter(j =>
    (j.title.toLowerCase().includes(txt)) && (loc=='' || j.loc===loc)
  );
  renderJobs(filtered);
}

renderJobs(jobs);
</script>
</body>
</html>
