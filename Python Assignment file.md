Steps/work-flow of the assignment:

1. Document Dr. X's function with comments and with markdown text in your Jupyter notebook.
2. Write a function that translates a string of nucleotides to amino acids based on Dr. X's pseudo-code suggestion.
3. Write an alternative translation function.
4. Write a function that calculates the molecular weight of each amino acid sequence.
5. Write a function that computes the GC-content of each DNA sequence.

 More manipulations of the data:
 
6. Add two new columns to the bears DataFrame: (1) molecular weight and (2) GC content.
7. Call your functions from step 3 (or step 2) and step 4 and 5 and fill in the new columns in the DataFrame.
 8. Plot a bar-chart of adult body mass per species. In your description of the graph, provide text that answers these questions: 
  a. What is the largest bear species?     b. What else is interesting about this species?
9. Plot a graph that shows the molecular weight as a function of GC content. 
10. Write the entire DataFrame to a new CSV file that includes your new columns.
11. BONUS: What other visualizations, functions or tasks would you do with this dataset? Add something interesting for fun. (0.5 additional points if your total score is < 15)

Improtant instructions to follow:
- Run all the code in Jupyter Notebook and push it to the repository
- Document everything properly so that it is easy to understand for the public
- The repository should contain only the relevant files, no additional files to be added

## TASK 1: Dr.X's function to retrieve sequences

def get_sequences_from_file(fasta_fn):
    sequence_data_dict = {}
    for record in SeqIO.parse(fasta_fn, "fasta"):
        description = record.description.split()
        species_name = description[1] + " " + description[2]
        sequence_data_dict[species_name] = record.seq
    return(sequence_data_dict)
    
  EXPLANATION:  : 
  def get_sequences_from_file(fasta_fn) : def is a user defined function that will help in extact the sequences from the fasta files  
  sequence_data-dict : creates empty directory named -sequence_data  
  description = record.description.split() : defines how to split the individual sequence files 
  sequence_data_dict[species_name] = record.seq : for every species_name, it assigns record.seq as the value  
  return(sequence_data_dict) : exits out and returns the sequences in the dictionary format
   
  ## TASK 2 : Write a function that translates a string of nucleotides to amino acids based on Dr. X's pseudo-code suggestion
 
 GIVEN ; All sequences start at codon position 1
 Complete a function that translates using a loop over the string of nucleotides  
 Here is  some pseudo-code and suggestions  
 feel free to change the function and variable names  
#def translate_function(string_nucleotides):   
     mito_table = CodonTable.unambiguous_dna_by_name["Vertebrate Mitochondrial"] # this should work using BioPython (be sure to check what this returns)  
     for-loop through every 3rd position in string_nucleotides to get the codon using range subsets  
        # IMPORTANT: if the sequence has a stop codon at the end, you should leave it off   
         # this is how you can retrieve the amino acid: mito_table.forward_table[codon]  
         add the aa to aa_seq_string  
     return(aa_seq_string)  
  
  Completing the function using for loop:
 def translate_function(string_nucleotides):  
    mito_table = CodonTable.unambiguous_dna_by_name["Vertebrate Mitochondrial"]    
    aa_string = ""     
    for x in range(0,len(string_nucleotides)-3, 3):    
        codon = string_nucleotides[x : x + 3]    
        aa_string = aa_string + mito_table.forward_table[codon]    
    return(aa_string)        
    
    
  ## TASK3: Alternative function using the translate function - Biopython library  
  
  from Bio.Seq import Seq
def translate3(sequence):
    coding_dna = Seq(sequence)
    sequence = coding_dna.translate(table="Vertebrate Mitochondrial", to_stop=True)
    return sequence

translate3('ATG')

## TASK 4: YOUR COUNT AA ANALYSIS FUNCTION
 
 code not working
 
 
 ## TASK 5: Count GC content
 
 dna_string = "ATGATCAACATCCGAAAAACTCATCCATTAGTTAAAATTATCAACAACTCATTCATTGACCTTCCAACACCATCAAACATTTCAACATGATGGAACTTTGGGTCCCTGTTAGGAGTGTGTCTGATCTTGCAAATCTTAACAGGCTTATTTCTAGCCATACACTATACATCAGATACAGCTACAGCCTTTTCATCAGTCGCACACATTTGTCGAGACGTCAACTATGGGTGATTTATCCGATATATACATGCCAATGGGGCCTCTATATTTTTTATCTGCCTATTTATACACGTAGGGCGAGGCTTATACTATGGATCATACCTATTTCCAGAGACATGGAATATCGGAATTATTCTCCTACTTACAATTATAGCCACCGCATTTATAGGATACGTCCTACCCTGAGGCCAAATGTCCTTCTGAGGAGCGACTGTCATCACCAACCTACTATCGGCCATTCCCTACATCGGAACGAACCTAGTAGAATGAATCTGAGGGGGCTTTTCCGTAGATAAGGCGACCCTAACACGATTCTTTGCTTTCCACTTTATCCTTCCATTTATCATCTCAGCACTAGCAATAGTCCATCTATTATTCCTTCACGAAACAGGATCTAATAACCCCTCCGGAATTCCATCTGACCCAGACAAAATCCCATTTTACCCCTATCATACAATTAAAGACATCCTAGGCGTCCTATTTCTTGTCCTCGCCTTAATAACCCTGGCTTTATTCTCACCAGACCTGTTAGGAGACCCTGATAACTATACCCCTGCAAATCCACTAAGTACCCCGCCACATATTAAGCCTGAATGGTACTTTCTATTTGCCTACGCTATCCTGCGATCCATTCCTAATAAACTAGGAGGGGTGCTAGCTCTAATCTTCTCTATTCTAATTCTAACTATTATTCCACTATTACATACATCCAAACAACGAAGCATGATATTCCGACCTCTAAGTCAATGCTTATTCTGACTCCTAGTAGCAGACCTACTCACACTAACATGAATTGGAGGACAGCCAGTAGAACACCCCTTCATTATTATTGGGCAATTGGCCTCTATTCTCTACTTTACAATTCTTCTAGTACTTATACCTATCACTAGCATTATTGAGAATAGCCTCTCAAAATGAAGA"

dna_list = list(dna_string)
print(dna_list)

dna_list.count("G")

gc_count = dna_list.count("G") + dna_list.count("c")
gc_frac = float(gc_count) / len(dna_list)
100 * gc_frac

14.473684210526317

Reference URL : https://www.tjelvarolsson.com/blog/python-for-biologists/


