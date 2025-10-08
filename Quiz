# Rebuild the quiz with images embedded as base64 (so they always display).
import os, base64, json, random

# Paths to embed
image_paths = [
    "/mnt/data/D60D02D3-A8F8-4F08-9EFD-F9BE548ADE0D.jpeg",
    "/mnt/data/D3196560-4BE2-437F-9F93-5F9B5B1D8B82.jpeg",
    "/mnt/data/E3F2C450-6C87-4F0F-B5FA-8732511EB65B.jpeg",
    "/mnt/data/3076E30B-638F-4C3C-865A-C640E655DDFA.jpeg",
    "/mnt/data/5A5D9E9C-25E2-433A-8A1C-31EBC9C74A01.jpeg",
    "/mnt/data/7B32AC35-E997-465C-9DBE-E05F5A6CBAB8.jpeg",
    "/mnt/data/515BBA2A-809E-4F97-9D05-4037157D1481.jpeg",
    "/mnt/data/94A00DF3-4822-4CB2-8BB7-418E82DB7D37.jpeg",
    "/mnt/data/83228E6D-2B17-4FFF-943E-217C8CC726ED.jpeg",
    "/mnt/data/IMG_6822.jpeg",
]

def to_data_uri(path):
    if not os.path.exists(path):
        return None
    with open(path, "rb") as f:
        b = f.read()
    mime = "image/jpeg"
    b64 = base64.b64encode(b).decode("ascii")
    return f"data:{mime};base64,{b64}"

data_uris = [to_data_uri(p) for p in image_paths]
data_uris = [u for u in data_uris if u]

# Core questions (shortened here by reusing the previous 50 base questions and 10 image ones)
base_questions = [
    {"q":"What is masonry?", "choices":["A type of foundation","A construction method using individual units laid in mortar","A roof system","A glazing system"], "answer":1, "explain":"Masonry uses bricks/blocks set in mortar to form walls."},
    {"q":"In brickwork, a horizontal row of bricks is called a:", "choices":["Wythe","Course","Header","Bond"], "answer":1, "explain":"A course is a horizontal layer; a wythe is a vertical layer."},
    {"q":"A vertical layer of bricks one unit thick is a:", "choices":["Wythe","Header","Sailor","Stretcher"], "answer":0, "explain":"A wythe is a continuous vertical section of masonry one unit thick."},
    {"q":"A brick laid with its long face showing along the wall length is a:", "choices":["Header","Soldier","Stretcher","Rowlock"], "answer":2, "explain":"A stretcher shows the long face; a header shows the short end."},
    {"q":"T/F: A masonry 'bond' is the waterproof layer behind brick.", "choices":["True","False"], "answer":1, "explain":"Bond is the pattern/arrangement of units tying wythes together."},
    {"q":"Vertically staggered masonry bonds generally:", "choices":["Reduce strength","Are only decorative","Improve strength and reduce cracking","Violate code"], "answer":2, "explain":"Staggered joints distribute loads and limit crack propagation."},
    {"q":"A load-bearing masonry wall:", "choices":["Carries only its own self-weight","Carries roof/floor loads above","Is always reinforced concrete","Is never exterior"], "answer":1, "explain":"Load-bearing walls transfer imposed loads to the foundation."},
    {"q":"CMU stands for:", "choices":["Concrete Masonry Unit","Composite Masonry Unit","Calcium Masonry Unit","Concrete Molded Unit"], "answer":0, "explain":"CMU = Concrete Masonry Unit (concrete block)."},
    {"q":"Which diagram component spans over an opening in masonry?", "choices":["Sill","Lintel","Jamb","Keyway"], "answer":1, "explain":"Lintels support loads above openings."},
    {"q":"T/F: Mortar joints can be profiled (e.g., concave, V, flush) and affect weathering.", "choices":["True","False"], "answer":0, "explain":"Joint profiles influence water shedding and durability."},
    {"q":"The primary purpose of a foundation system is to:", "choices":["Provide aesthetics","Transfer building loads safely to the ground","Control interior temperature","House electrical panels"], "answer":1, "explain":"Foundations collect and spread loads to soil/rock within bearing capacity."},
    {"q":"Live loads are best described as:", "choices":["Permanent building weight","Movable/transient loads like people and furniture","Wind pressure","Seismic forces"], "answer":1, "explain":"Live loads vary with occupancy; dead loads are permanent."},
    {"q":"A concentrated load is:", "choices":["Evenly distributed over an area","Applied at a point or small area","Always a wind load","Only in roof design"], "answer":1, "explain":"Point/small area loads cause higher local stresses."},
    {"q":"Uniform load means:", "choices":["Load varies along the span","Load is zero at midspan","Load is constant per unit length/area","Only applies to wind"], "answer":2, "explain":"Uniform loads are constant along a member or surface."},
    {"q":"Static load vs Dynamic load:", "choices":["Static varies rapidly; dynamic is constant","Static is constant/slowly varying; dynamic varies with time/inertia effects","Both are the same","Dynamic loads exclude seismic"], "answer":1, "explain":"Dynamic loads (wind, seismic) involve acceleration/inertia."},
    {"q":"Tensile stress is associated with:", "choices":["Pushing together","Pulling apart","Sliding layers","Torsion only"], "answer":1, "explain":"Tension stretches material fibers."},
    {"q":"Compressive stress is associated with:", "choices":["Pushing together","Pulling apart","Sliding layers","Thermal expansion only"], "answer":0, "explain":"Compression shortens/squeezes fibers."},
    {"q":"Shear occurs when:", "choices":["Two opposing forces act parallel to a plane","Material is twisted only","Only axial loads exist","Only temperature changes occur"], "answer":0, "explain":"Shear is sliding between adjacent planes from opposing parallel forces."},
    {"q":"In simple bending of a beam, the TOP fibers are in _____ and the BOTTOM in _____.", "choices":["Tension; compression","Compression; tension","Shear; torsion","Static; dynamic"], "answer":1, "explain":"Top shortens (compression); bottom lengthens (tension)."},
    {"q":"T/F: Stability of a structure means forces are equal to zero.", "choices":["True","False"], "answer":1, "explain":"Equilibrium means sums are balanced, not zero forces; the study guide flags 'forces equal to' as false."},
    {"q":"Which is NOT a primary structural system by form?", "choices":["Load-bearing wall","Post-and-beam (frame)","Shell/surface","Electrical"], "answer":3, "explain":"Electrical is a service system, not a structural system."},
    {"q":"Four primary characteristics of a structural system include:", "choices":["Aesthetics, color, pattern, texture","Strength/stiffness, stability, economy, serviceability","Fire rating, R-value, U-factor, SHGC","Span, pitch, soffit, fascia"], "answer":1, "explain":"From the notes: stiffness/strength, stability, economy (and serviceability)."},
    {"q":"Which foundation is least typical for small residential structures?", "choices":["Slab-on-grade","Basement","Crawl space","Caisson"], "answer":3, "explain":"Caissons are deep foundations for heavy/complex loads."},
    {"q":"A crawlspace foundation is:", "choices":["No space between ground and slab","A short raised space allowing access below the floor","A deep drilled pier","An above-grade slab"], "answer":1, "explain":"Crawlspaces allow access to utilities and ventilation below floors."},
    {"q":"Slab-on-grade means:", "choices":["Suspended concrete slab above ground","Concrete poured into formwork directly on prepared ground with no crawlspace","Wood platform on piers","Precast planks on beams"], "answer":1, "explain":"Concrete slab cast directly at grade; no space below."},
    {"q":"T/F: All buildings settle over time.", "choices":["True","False"], "answer":0, "explain":"Some settlement is normal; differential settlement is problematic."},
    {"q":"Differential settlement is:", "choices":["Uniform downward movement","Non-uniform movement causing distortion/cracking","Uplift due to wind","Thermal expansion"], "answer":1, "explain":"Different amounts of settlement cause angular distortion."},
    {"q":"A pile foundation is:", "choices":["Shallow spread footing","Deep element driven/drilled to transfer load to deeper strata","Only for lightweight buildings","Same as slab-on-grade"], "answer":1, "explain":"Piles bypass weak near-surface soils to stronger layers."},
    {"q":"Lateral forces on foundations can come from:", "choices":["Hydrostatic soil pressure","Wind","Seismic","All of the above"], "answer":3, "explain":"Soil water, wind, and seismic all impose lateral loads."},
    {"q":"What construction method replaced balloon framing for most housing?", "choices":["Heavy timber","Platform framing","Post-and-beam","Masonry bearing"], "answer":1, "explain":"Platform (Western) framing uses floor platforms between stories."},
    {"q":"Cripple studs are used to:", "choices":["Brace roof rafters","Frame short segments above/below openings","Support floor joists","Anchor sill plates"], "answer":1, "explain":"Cripples fill above/below windows and doors."},
    {"q":"A header in wood framing:", "choices":["Is the base plate at floor","Carries loads over an opening","Is a roof ridge board","Is a joist hanger"], "answer":1, "explain":"Headers transfer loads to trimmers/kings."},
    {"q":"Basic parts of a steel stud include:", "choices":["Web, flanges, return lips","Chord, web, seat","Top chord, bottom chord, web","Stud, plate, shim"], "answer":0, "explain":"Cold-formed C-stud geometry uses web, flanges, and small return lips."},
    {"q":"T/F: Steel stud partitions can be load-bearing or non-load-bearing depending on gauge and design.", "choices":["True","False"], "answer":0, "explain":"Heavier gauges with proper design can be load-bearing."},
    {"q":"Sheathing on framed walls primarily:", "choices":["Provides insulation value","Resists racking (lateral) and adds diaphragm stiffness","Acts as finished cladding","Replaces the air/water barrier"], "answer":1, "explain":"Plywood/OSB sheathing braces walls against lateral loads."},
    {"q":"Which of the following is a precast concrete floor member?", "choices":["Slab-on-grade","Double T","Cast-in-place flat plate","Site strip footing"], "answer":1, "explain":"Double T and single T are factory precast elements."},
    {"q":"Which is NOT precast?", "choices":["Hollow-core slab","Single T","Cast-in-place slab","Double T"], "answer":2, "explain":"Cast-in-place is formed and poured on site."},
    {"q":"Roof shapes include all EXCEPT:", "choices":["Gable","Hip","Gambrel","Wythe"], "answer":3, "explain":"A wythe is a masonry term, not a roof shape."},
    {"q":"Three common roof framing materials are:", "choices":["Wood, steel, concrete","Brick, wood, glass","Bamboo, steel, CMU","Gypsum, wood, aluminum"], "answer":0, "explain":"Roofs can be framed with wood trusses, steel, or concrete."},
    {"q":"In a stucco-over-wood-stud exterior wall, which layer is the primary drainage plane?", "choices":["Continuous insulation","Air/water barrier (WRB)","Gypsum sheathing","Reinforcing mesh"], "answer":1, "explain":"WRB manages bulk water behind the cladding."},
    {"q":"Continuous exterior insulation primarily improves:", "choices":["Structural strength","Thermal performance and condensation control","Acoustic reflection","Electrical bonding"], "answer":1, "explain":"CI reduces thermal bridges and helps keep sheathing warm/dry."},
    {"q":"Concrete composition typically includes:", "choices":["Cement, sand, coarse aggregate, water (and admixtures)","Clay, sand, water","Gypsum, lime, sand, water","Epoxy, fibers, paint"], "answer":0, "explain":"Standard concrete = binder (cement), fine/coarse aggregates, water."},
    {"q":"Concrete reaches design compressive strength at approximately:", "choices":["7 days","14 days","21 days","28 days"], "answer":3, "explain":"Specified strength f'c is referenced at 28 days."},
    {"q":"T/F: Fresh slabs can usually be walked on after ~24 hours, but full strength takes weeks.", "choices":["True","False"], "answer":0, "explain":"Initial set allows careful foot traffic; strength gain continues."},
    {"q":"Why is an airlock (vestibule) desirable in cold/windy climates?", "choices":["For decoration","To reduce infiltration and heat loss when doors open","To store deliveries","To meet egress width"], "answer":1, "explain":"Airlocks buffer pressure/temperature, reducing energy loss."},
    {"q":"How do windows impact interior needs?", "choices":["Only by adding glare","They affect daylight, views, heat gain/loss, and glare control","They only affect acoustics","They have no impact"], "answer":1, "explain":"Windows influence lighting, comfort, and energy use."},
    {"q":"In the Northern Hemisphere, which façade generally receives the most consistent solar exposure?", "choices":["North","South","East","West"], "answer":1, "explain":"South gets the most annual sun; east = morning, west = afternoon/overheating."},
    {"q":"Glare is best defined as:", "choices":["Even, comfortable illumination","Excessive brightness contrast causing visual discomfort/reduced visibility","A reflected image of the lamp","Any daylight"], "answer":1, "explain":"Glare reduces visual performance; design aims to avoid it."},
    {"q":"T/F: We generally want glare in workplaces.", "choices":["True","False"], "answer":1, "explain":"Glare is undesirable; control with shading, surface finishes, and layout."},
    {"q":"Most effective first step to reduce fossil-fuel reliance in buildings:", "choices":["Add decorative lighting","Increase envelope efficiency and reduce demand (insulation/air sealing, passive design)","Install larger cooling systems","Paint walls darker"], "answer":1, "explain":"Efficiency and load reduction come before renewables ('load first')."},
    {"q":"Straw-bale construction uses:", "choices":["Compressed straw bales as wall infill/insulation","Bamboo poles as trusses","Only CMU blocks","Metal studs with spray foam"], "answer":0, "explain":"Straw bales provide thick, insulating walls with plaster skins."},
    {"q":"Bamboo construction is valued for:", "choices":["Low tensile strength","Rapid renewability and high strength-to-weight","Incompatibility with structures","Only decorative uses"], "answer":1, "explain":"Bamboo is strong, light, and rapidly renewable (with proper detailing)."},
    {"q":"A gabion wall consists of:", "choices":["Hollow concrete planks","Wire baskets filled with rock","Plastic honeycomb","CMU with grout"], "answer":1, "explain":"Gabions are cages filled with stones—used for retaining/erosion control and aesthetic walls."},
    {"q":"ICF (Insulated Concrete Forms) are:", "choices":["Factory precast concrete slabs","Foam block forms filled with concrete to create insulated walls","Only floor insulation panels","Wood forms reused for slabs"], "answer":1, "explain":"ICF uses permanent foam forms as insulation + concrete core."},
    {"q":"SIPs (Structural Insulated Panels) are:", "choices":["Steel deck with concrete topping","Foam core sandwiched between structural facings (e.g., OSB)","CMU with rigid insulation","Only interior acoustic panels"], "answer":1, "explain":"SIPs combine structure + insulation in factory-made panels."},
    {"q":"Biocomposites are:", "choices":["Pure metals","Concrete-only materials","Composites with bio-based components (e.g., fibers/resins)","Only bamboo poles"], "answer":2, "explain":"They use renewable/bio-based constituents to reduce environmental impact."},
    {"q":"What did your class identify as the most important aspect of construction?", "choices":["Scheduling","Communication","Software selection","Material cost"], "answer":1, "explain":"Per the study guide, communication."},
    {"q":"Historic traditional material widely used in older U.S. buildings:", "choices":["Carbon fiber","Reinforced plastics","Stone and brick","ETFE foil"], "answer":2, "explain":"Historic systems relied heavily on masonry/stone."},
    {"q":"Ballast in roofing typically refers to:", "choices":["Counterweight (e.g., gravel) holding down roofing membranes","Electrical grounding","Thermal insulation","Acoustic damping"], "answer":0, "explain":"Ballast weighs down loose-laid membranes (and provides UV protection)."},
    {"q":"Common species for solid-sawn structural timber include:", "choices":["Douglas fir–larch and Southern Pine","Teak and Ebony","Balsa and Cork","Bamboo and Hemp"], "answer":0, "explain":"These species are common in North American construction."},
    {"q":"Major building systems are traditionally divided into:", "choices":["Plumbing, electrical, HVAC (and others)","Foundations, façades, interiors only","Only architectural finishes","Only IT systems"], "answer":0, "explain":"Service systems include plumbing, electrical, HVAC, etc."},
    {"q":"A cantilever is a member that:", "choices":["Is supported at both ends","Is simply supported midspan","Projects beyond its support with a free end","Can’t carry bending"], "answer":2, "explain":"Cantilevers are fixed at one end and free at the other."},
    {"q":"A catenary describes the ideal shape of:", "choices":["A beam in bending","A freely hanging cable under its own weight","A rigid arch under compression","A column under buckling"], "answer":1, "explain":"Hanging cables take the catenary shape; inverted, it is efficient for compression arches."},
    {"q":"An arch primarily carries:", "choices":["Tension only","Compression along its curve with lateral thrust at supports","Pure shear","Bending only"], "answer":1, "explain":"Arches transfer compression to supports producing horizontal thrust."},
    {"q":"Site considerations typically include FOUR broad categories such as:", "choices":["Topography, climate/sun/wind, access/orientation, vegetation/water","Wall color, furniture style, brand palette, signage size","Only zoning","Only parking"], "answer":0, "explain":"These factors influence building form and interior conditions."},
    {"q":"Windows can reduce reliance on electric lighting primarily by:", "choices":["Increasing glare","Providing daylight that is controlled and distributed appropriately","Blocking all sun","Only being small"], "answer":1, "explain":"Daylight (with shading/controls) reduces artificial lighting loads."},
    {"q":"T/F: Platform framing builds one full-height wall from ground to roof without breaks.", "choices":["True","False"], "answer":1, "explain":"That describes balloon framing. Platform framing stacks floor platforms story by story."},
    {"q":"T/F: Differential settlement can cause sloped floors and cracked finishes.", "choices":["True","False"], "answer":0, "explain":"Non-uniform settlement distorts structure and finishes."},
    {"q":"Which is a function of a lintel?", "choices":["Ventilation","Span over an opening to carry loads","Waterproofing","Decoration only"], "answer":1, "explain":"Lintels are structural beams over openings."},
]

# Build 10 image-based questions using the embedded data URIs
concept_pairs = [
    ("Looking at this image, which BEST describes the structural concept illustrated?", ["Load-bearing masonry wall", "Curtain wall on steel frame", "Balloon framing", "Cable-stayed roof"], 0, "Stacked masonry units transferring vertical loads to foundation."),
    ("This image relates MOST closely to which wall layer/function?", ["Air/Water Barrier (WRB)", "Gypsum board finish", "Decorative veneer only", "Foundation waterproofing"], 0, "The WRB is the primary drainage plane behind cladding."),
    ("Which framing term is MOST associated with the component spanning an opening here?", ["Sill plate", "Header/Lintel", "Ridge board", "King stud"], 1, "Headers/lintels carry loads over openings."),
    ("Which load type is MOST relevant for the scenario shown?", ["Live load", "Dead load", "Lateral load", "Thermal load"], 2, "Wind/soil pressure → lateral loads."),
    ("This picture MOST likely corresponds to:", ["Platform framing", "Balloon framing", "Post-and-beam with infill", "Waffle slab"], 0, "Platform framing is standard in modern light-frame construction."),
    ("The joint profile emphasized here primarily affects:", ["Shear strength", "Weathering and water shedding", "Acoustic absorption", "Electrical continuity"], 1, "Mortar joint profiles influence durability against water intrusion."),
    ("What type of concrete system does this MOST likely represent?", ["Cast-in-place slab", "Precast Double T", "Hollow-core precast plank", "Raised access floor"], 1, "T-shaped precast members indicate Single/Double T systems."),
    ("Which statement is MOST accurate for the roof detail shown?", ["Roofs never need sheathing", "Sheathing provides diaphragm action and nail base", "Ridge boards carry vertical loads alone", "Underlayment is purely decorative"], 1, "Sheathing braces the assembly and is a nailing substrate."),
    ("Which foundation concept is MOST applicable here?", ["Crawlspace", "Caisson/pile", "Slab-on-grade", "Mat foundation"], 2, "Thickened slab at perimeter with no space below suggests slab-on-grade."),
    ("This figure supports which SITE/DAYLIGHT idea?", ["South façades receive the least annual sun", "East = morning sun, West = afternoon heat", "North is hottest", "Orientation has no impact"], 1, "East brings morning sun; west tends to overheat in afternoons."),
]

image_questions = []
for i, (stem, choices, ans, exp) in enumerate(concept_pairs):
    img = data_uris[i] if i < len(data_uris) else None
    if img:
        image_questions.append({
            "q": stem, "choices": choices, "answer": ans, "explain": exp, "image": img
        })

random.seed(33)
base_pick = random.sample(base_questions, 50)
all_qs = base_pick + image_questions
random.shuffle(all_qs)
all_qs = all_qs[:60]

html = f"""
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Exam 1 — Interactive Quiz with Embedded Images (60 Qs)</title>
<style>
  :root {{ --bg:#0b0c10; --card:#15181d; --ink:#eaf2f2; --muted:#9fb1b7; --accent:#89c2ff; --right:#1fbf75; --wrong:#ff5d73; }}
  html,body{{margin:0;padding:0;background:var(--bg);color:var(--ink);font-family:Inter,system-ui,-apple-system,Segoe UI,Roboto,Helvetica,Arial,sans-serif;line-height:1.55;}}
  .wrap{{max-width:980px;margin:32px auto;padding:0 16px;}}
  h1{{font-size:28px;margin:0 0 6px;}}
  .sub{{color:var(--muted);margin-bottom:18px}}
  .controls{{display:flex;gap:10px;flex-wrap:wrap;margin:16px 0 22px 0;}}
  .btn{{background:#212631;border:1px solid #2a2f37;padding:10px 14px;border-radius:10px;color:var(--ink);cursor:pointer}}
  .btn:hover{{border-color:#3b4350}}
  .pill{{display:inline-block;background:#1d2330;border:1px solid #30394a;color:var(--muted);padding:6px 10px;border-radius:999px;margin-left:8px;font-size:12px}}
  .card{{background:var(--card);border-radius:14px;padding:16px 16px 12px;margin:12px 0;box-shadow:0 10px 30px rgba(0,0,0,.25);}}
  .q{{font-weight:700;margin-bottom:10px}}
  .pic{{margin:8px 0 10px 0; border-radius:12px; overflow:hidden; border:1px solid #2a2f37;}}
  .pic img{{display:block;width:100%;height:auto;object-fit:contain; background:#0f1216;}}
  .choice{{display:block;margin:8px 0;padding:10px 12px;border:1px solid #2a2f37;border-radius:10px;cursor:pointer;transition:.15s;}}
  .choice:hover{{border-color:#3b4350;transform:translateY(-1px);}}
  .choice.correct{{background:rgba(31,191,117,.12);border-color:var(--right);}}
  .choice.incorrect{{background:rgba(255,93,115,.12);border-color:var(--wrong);}}
  .explain{{color:var(--muted);margin-top:8px;display:none}}
  .sticky{{position:sticky;top:0;background:linear-gradient(180deg, rgba(11,12,16,0.95), rgba(11,12,16,0.75));backdrop-filter:blur(6px);z-index:99;padding:8px 0;margin-bottom:8px}}
  .summary{{background:#12151a;border:1px dashed #2a2f37;border-radius:12px;padding:14px;margin:20px 0;color:var(--muted)}}
  .summary .big{{font-size:20px;color:var(--ink);font-weight:800}}
</style>
</head>
<body>
<div class="wrap">
  <div class="sticky">
    <h1>Exam 1 — Interactive Quiz with Embedded Images</h1>
    <div class="sub">60 questions • MC + True/False • Instant feedback & explanations • Randomized on load • Images embedded for reliable display</div>
    <div class="controls">
      <button class="btn" id="shuffle">🔀 Shuffle</button>
      <button class="btn" id="reset">↩️ Reset</button>
      <div class="pill">Score: <span class="score" id="score">0</span>/<span id="answered">0</span> • Total: <span id="total">0</span></div>
    </div>
  </div>
  <div id="quiz"></div>
  <div id="final" class="summary" style="display:none;">
    <div class="big" id="finalText">Final Score</div>
    <div id="tips">Tip: use Shuffle to re-order and reinforce weak topics.</div>
  </div>
  <div class="summary">Made for Tracy 💚 • Based on your Exam #1 study guide & lecture notes.</div>
</div>
<script>
const RAW = {json.dumps(all_qs, ensure_ascii=False)};
let DATA = [];
let score = 0, answered = 0;
const quizEl = document.getElementById('quiz');
const scoreEl = document.getElementById('score');
const ansEl = document.getElementById('answered');
const totalEl = document.getElementById('total');
const finalBox = document.getElementById('final');
const finalText = document.getElementById('finalText');

function shuffleArray(arr){{ for(let i=arr.length-1;i>0;i--){{ const j=Math.floor(Math.random()*(i+1)); [arr[i],arr[j]]=[arr[j],arr[i]]; }} }}

function prep(){{
  DATA = JSON.parse(JSON.stringify(RAW));
  // Randomize on load
  shuffleArray(DATA);
  // Shuffle MC choices
  DATA.forEach(item=>{{
    if(item.choices.length>2){{
      const indexed = item.choices.map((c,i)=>({{c,i}}));
      shuffleArray(indexed);
      item.choices = indexed.map(o=>o.c);
      item.answer = indexed.findIndex(o=>o.i===item.answer);
    }}
  }});
}}

function render(){{
  quizEl.innerHTML='';
  totalEl.textContent = DATA.length;
  score=0; answered=0;
  scoreEl.textContent=0; ansEl.textContent=0;
  finalBox.style.display='none';
  DATA.forEach((item, idx)=>{{
    const card = document.createElement('div');
    card.className='card';
    const q = document.createElement('div'); q.className='q'; q.textContent=(idx+1)+'. '+item.q; card.appendChild(q);
    if(item.image) {{
      const pic = document.createElement('div'); pic.className='pic';
      const img = document.createElement('img'); img.src = item.image; img.alt="question image";
      pic.appendChild(img); card.appendChild(pic);
    }}
    item.choices.forEach((c,ci)=>{{
      const ch=document.createElement('div'); ch.className='choice'; ch.textContent=(item.choices.length===2?['T','F'][ci]:String.fromCharCode(65+ci))+'. '+c;
      ch.addEventListener('click', ()=>{{
        if(ch.classList.contains('correct')||ch.classList.contains('incorrect')) return;
        const already = card.querySelectorAll('.choice.correct, .choice.incorrect').length>0;
        if(ci===item.answer){{ ch.classList.add('correct'); if(!already){{score++; answered++;}}}}
        else{{ ch.classList.add('incorrect'); const all=card.querySelectorAll('.choice'); all[item.answer].classList.add('correct'); if(!already){{answered++;}}}}
        const ex=card.querySelector('.explain'); if(ex){{ex.style.display='block';}}
        scoreEl.textContent=score; ansEl.textContent=answered;
        if(answered===DATA.length){{ showFinal(); }}
      }});
      card.appendChild(ch);
    }});
    const ex=document.createElement('div'); ex.className='explain'; ex.textContent='Why: '+(item.explain||''); card.appendChild(ex);
    quizEl.appendChild(card);
  }});
}}

function showFinal(){{
  const pct = Math.round((score/ DATA.length)*100);
  finalText.textContent = `Final Score: ${'{'}score{'}'}/${'{'}DATA.length{'}'} = ${'{'}pct{'}'}%`;
  finalBox.style.display='block';
}}

document.getElementById('shuffle').addEventListener('click', ()=>{{ prep(); render(); }});
document.getElementById('reset').addEventListener('click', ()=>{{ render(); }});
prep(); render();
</script>
</body>
</html>
"""

out_path = "/mnt/data/Exam1_Interactive_Quiz_with_Embedded_Images.html"
with open(out_path, "w", encoding="utf-8") as f:
    f.write(html)

out_path
