#importing requests module
import requests

#making a list of Uniprot accession numbers
accession_numbers = ['P04439', 'Q4TVV3', 'P10814', 'Q05744']

#creating the base URL for UniProt API
base_url = "https://rest.uniprot.org/uniprotkb/"

#creating a dictionary to store results
info = {}

#createing a for loop to go through each accession number and fetch data
for accession in accession_numbers:
    #building the URL for the API request
    url = f"{base_url}{accession}.json"
    
    #making the GET request
    response = requests.get(url)
    
    if response.status_code == 200:  #checking if the response is valid
        try:
            #parsing the response as JSON file
            data = response.json()
            
            #extracting the protein name
            protein_name = data.get("proteinDescription", {}).get("recommendedName", {}).get("fullName", {}).get("value", "Unknown")
            
            #extracting the scientific name of the organism
            scientific_name = data.get("organism", {}).get("scientificName", "Unknown")
            
            #saving the result
            info[accession] = {
                "protein_name": protein_name,
                "scientific_name": scientific_name
            }
        except requests.JSONDecodeError:
            print(f"Failed to parse JSON for {accession}.")
    else:
        print(f"Failed to fetch data for {accession}. Status code: {response.status_code}")

#printing the output
for accession, details in info.items():
    print(f"For {accession}, the protein name is {details['protein_name']}, and the scientific name of the organism is {details['scientific_name']}.")
