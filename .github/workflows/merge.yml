const fs = require('fs');

const files = fs.readdirSync('.').filter(f => 
  f.endsWith('.json') && 
  f !== 'uk_locations_master.json' &&
  (f.startsWith('uk_industrial_locations') || f.startsWith('gemini-code'))
);

let all = [];
for (const file of files) {
  try {
    const data = JSON.parse(fs.readFileSync(file, 'utf8'));
    if (Array.isArray(data)) all = all.concat(data);
    console.log('Loaded ' + file + ' (' + (Array.isArray(data) ? data.length : 0) + ' locations)');
  } catch(e) {
    console.log('Skipping ' + file + ': ' + e.message);
  }
}

const seen = new Set();
const unique = all.filter(item => {
  if (seen.has(item.slug)) return false;
  seen.add(item.slug);
  return true;
});

unique.sort((a, b) => a.slug.localeCompare(b.slug));
fs.writeFileSync('uk_locations_master.json', JSON.stringify(unique, null, 2));
console.log('Done. ' + unique.length + ' unique locations written to uk_locations_master.json');
