**Performance Model - Real Problem**
• Problem:  
	• You're simulating something like the Krakatau ash plume.  
	• There are many materials (e.g. types of ash), but only a few per cell in the  
mesh grid.  
• Challenge:  
	• If you store data for every material in every cell, you're wasting memory  
	and time.  
	• So, can we store only non-zero or present materials efficiently?

**Use a Compressed Sparse Representation**
• This means you:  
	• Only store materials that are actually present in a cell.  
	• Avoid allocating memory for unused spots.  
• Result:  
	• Memory savings > 95%  
	• Speed improvement ~90%  
	• Models predicted performance within 20–30% of real measurements.  
	• But it comes with a cost: the code becomes harder to write and maintain.

**How to Decide if It’s Worth It?**  
• Use a Simple Performance Model:  
	• Count memory loads/stores (memops)  
	• Count floating point ops (flops)  
	• Check if memory is contiguous  
	• Consider branches (if-statements) and small loops  
	• Use hardware data (like bandwidth or cache size)

**Compressed sparse data structure**
• In simulations (like for a volcano or fluid flow), each grid cell can have one or more  
materials (e.g., ash types, fluids, gases).  
• In sparse cases, most cells contain only one material, and only a few (like cell 7)  
contain multiple materials.  
• If you store all materials in all cells, you:  
• Waste memory (because most are empty)  
• Slow down performance (more memory to load)  
• The better approach is to use a compressed sparse data structure:  
Store only the materials that are actually present in each cell.

**Two Key Calculations (Representative Kernels):**
• ρavg[C]: Average density for each cell  
	• Adds up the densities of all materials in a cell, then averages  
	• This gives you a per-cell value  
• p[C][m]: Pressure for each material using ideal gas law  
	• Calculated using p = nRT/v  
	• This gives you a per-material-per-cell value

Key Terms:
• Arithmetic intensity ≤ 1 flop/word -> Very few calculations per memory  
access  
• This means these are bandwidth-limited problems (limited by how fast  
memory can move, not how fast CPU can calculate)

**Two Datasets**
Geometric Shapes Problem  
• Mesh is filled with neat rectangles of materials  
• 95% of cells are pure (1 material)  
• 5% of cells are mixed (multiple materials)  
• There’s some data locality (similar data is near each other)  
• Estimated branch prediction miss = 0.7

**Randomly Initialized Mesh**
Scenario  
• Mesh Composition:  
• 80% pure cells, 20% mixed cells  
• Low data locality  
• Branch prediction miss: Bp = 1.0

**Two Key Design Dimensions**
• Data Layout  
	• Cell-centric: organized by cell  
	• Material-centric: organized by material  
	• Affects memory stride and cache behavior  
• Loop Order  
	• Cell-dominant loop: outer loop over cells  
	• Material-dominant loop: outer loop over materials  
	• Affects access patterns

**Performance Insight**
• Best performance occurs when:  
- Data layout ↔ Loop order match
• Trade-off:  
	• One kernel may favor a cell-based layout  
	• Another may favor a material-based layout  
• No one-size-fits-all — tune per kernel  

