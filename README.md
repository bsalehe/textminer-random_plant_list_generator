# Textminer-random_list_generator

This is  a Python based tool for manipulation of lists to create random files samples.

The manipulation required:

- Find random sample selection of the plant species from the population list (PS) of the area.

- Find random sample selection of the real sample and compare with PS.

- Find which plants are significantly more common between real samples and null samples in each area.

## Detail on input files required
Input files:
- 118 county plant lists (names of the files = county names). These files are lists of species (variable “species”) and their abundance (variable “freq”) 
- Null sample size list per county (name of the file = “null_size_per_county.xlsx”) and their area (being Celtic, Viking, Anglo-Saxon, and Viking&Anglo-Saxon in the variable ‘area’)
- Medicinal plant list (name of the file = “medicinals.xlsx”. This lists 348 plants with the number of counties where they are used according to area: Celtic, Viking, Anglo-Saxon, and Viking&Anglo-Saxon)
- Medicinal plants per county (medicinal_plants_per_county.xlsx); shows which plants are used in each county

## Detail on what the tool does/required to do
Script:

- Remove duplicates from the 118 county plant lists.
- Filter out plants that are NOT in the medicinals list from each of the 118 county plant lists. -> output1 = 118 county files with fewer plants.
- For each new county file create 100 random lists of plants (“null populations”) of the size indicated in “null_size_per_county.xlsx”. These random lists should:
 
	Take into account plant abundance (so, if a plant has a “freq” of 50, it has 50 more chances to get into a null population).

	Each null population does not have repeated plant names (sampling without replacement).

	Output2: 100 random plant lists per county (so, 11800 “null samples” in total).

	Summarise results: Per each county, a summary of the null populations. Compile all the plants in the 100 null populations in a list, with a variable indicating the number of times they appear in these random lists (so, 0-100 times). Add a column where these frequencies are divided by 100, this is the frequency column->output3 118 files, one for each county, with values between 0-100 (one column) and 0-1 (the frequencies column) for each plant species in that county.

	Create a file for each plant species which lists all the counties and shows i. whether the plant is in each county (this information comes from the 118 county list files); ii. if the plant is medicinal or not in each county (present or absent of use as a medicinal plant, info in “medicinal_plants_per_county.xlsx”), and iii. the frequency in the null (from output3) ->output4 (348 medicinal plants, so 348 files)

	Create a new file for each plant that groups information per area (Celtic, Viking, Anglo-Saxon, and Viking&Anglo-Saxon, see areas in “null_size_per_county.xlsx”). Per plant (348 files) show, i. number of counties in each area where it is present, ii. number of counties in each area where it is medicinal (info in “medicinals.xlsx”), iii. add the frequencies in the null from output4 per each area divided by the number of counties in that area. -> output5

