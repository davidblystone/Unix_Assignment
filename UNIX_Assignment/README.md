Assignment 1: Unix 

Part 1
‘’’
wc fang_et_al_genotypes.txt 
‘’’
tells me the number of lines, words, and bytes that are in the fang_et_al_genotypes.txt file. I see there is 2783 lines, 2744038 words, and 11051939 bytes


‘’’
head -n1 fang_et_al_genotypes.txt  
‘’’

                          # lets me see the first line of the file, but even this is too congested to see what is going on with the file.  I can there are various columns ranging from the sample id to different marker names.  I can also see SNP locations that are missing genotypic data.  
‘’’  
awk -F"\t" '{print NF; exit}' fang_et_al_genotypes.txt
‘’’
    #This code tells me the number of columns that are in this fang_et_al_genotypes.txt file.  We can see is an extremely wide file with 986 columns, and 2783 rows.  

986
‘’’
wc snp_position.txt 	

‘’’
						              # This code tells me the number of lines, words, and bytes that are in the snp_position.txt. There are 984 lines, 13198 words, and 82763 bytes in this file.  

984 13198 82763 snp_position.txt

‘’’
head -n1 snp_position.txt 
‘’’

SNP_ID	cdv_marker_id	Chromosome	Position	alt_pos mult_positions	amplicon	cdv_map_feature.name	gene	candidate/random	Genaissance_daa_id	Sequenom_daa_id	count_amplicons	count_cmf	count_gene   

   # This code shows the headers of the file. We can clearly see that there are 15 columns in this file.  From this header, we can see that this file contains the specific information about each respective SNP marker, including chromosome, position, candidate genes, and number of genes, etc. 
	

Part 2
‘’’
awk '{ print $1,$3,$4}' snp_position.txt > reordered_snp_position.txt                             
‘’’
#This code rearranges the columns of the snp_position.txt file so that the order is SNP_ID Chromosome Position
‘’’
awk -F, '$3==ZMM' fang_et_al_genotypes.txt > maize_genotypes.txt  
‘’’
                                         # This code creates a new file from the fang_et_al_genotypes.txt with only the rows that contains at least ZMM in the group column for maize.
‘’’
awk -F, '$3==ZMP' fang_et_al_genotypes.txt > teosinte_genotypes.txt   
‘’’
                                     # This code creates a new file from the fang_et_al_genotypes.txt with only the rows that contains at least ZMP in the group column for teosinte.
 ‘’’                  
sort -k1,1 reordered_snp_position.txt >sorted_reordered_snp_position.txt                               
‘’’
    #this code sorts the first column snp_id and creates it as a new file for eventual merging

‘’’
awk -f transpose.awk teosinte_genotypes.txt > transposed_teosinte_genotypes.txt                         
‘’’
    # This code transposes the teosinte genotype file so that it can eventually be joined with the reordered_snp_position.txt file
‘’’
awk -f transpose.awk maize_genotypes.txt > transposed_maize_genotypes.txt                                 
‘’’
  # This code transposes the maize genotype file so that it can eventually be joined with the reordered_snp_position.txt file




‘’’
sort -k1,1 transposed_maize_genotypes.txt  > sorted_transposed_maize_genotypes.txt                
‘’’
          # This code sorted the new transposed first column of the maize file which is essentially the snp_id column just like with the snp_position file for merging
‘’’
join -1 1 -2 1 sorted_reordered_snp_position.txt sorted_transposed_maize_genotypes.txt > joined_maize.txt 
‘’’
   # this code joins the two sorted txt files for maize together. The syntax states that the first column is the key to join the first file. And the first column will be the key to join in the second file. Which are both the snp_id columns now.

‘’’
sort -k1,1 transposed_teosinte_genotypes.txt  > sorted_transposed_teosinte_genotypes.txt            
‘’’
         #This code sorted the new transposed first column of the teosinte file which is essentially the snp_id column just like with the snp_position file for merging
‘’’
join -1 1 -2 1 sorted_reordered_snp_position.txt sorted_transposed_teosinte_genotypes.txt > joined_teosinte.txt   
‘’’
 # this code joins the two sorted txt files for teosinte together. The syntax states that the first column is the key to join the first file. And the first column will be the key to join in the second file. Which are both the snp_id columns now.

## For Maize

#File type 1 chromosome 1 maize
‘’’
awk '$2 == 1' joined_maize.txt  > chromosome_1_joined_maize.txt                                             
 #this code uses awk to select rows that contain chromosome 1 

sort -k3,1 -r chromosome_1_joined_maize.txt > increasing_chromosome_1_joined_maize.txt                      
 #this code sorts the file in increasing chromosome position in column 3
sed ’s/-t/?/‘ increasing_chromosome_1_joined_maize.txt  > encoded_increasing_chromosome_1_joined_maize.txt
‘’’
#File type 1 chromosome 2 maize
‘’’
awk '$2 == 2’ joined_maize.txt  > chromosome_2_joined_maize.txt                                              
#this code uses awk to select rows that contain chromosome 2 
sort -k3,1 -r chromosome_2_joined_maize.txt > increasing_chromosome_2_joined_maize.txt                       
#this code sorts the file in increasing chromosome position in column 3
sed ’s/-t/?/‘ increasing_chromosome_2_joined_maize.txt  > encoded_increasing_chromosome_2_joined_maize.txt
‘’’
#File type 1 chromosome 3 maize
‘’’
awk '$2 == 3’ joined_maize.txt  > chromosome_3_joined_maize.txt                                             
 #this code uses awk to select rows that contain chromosome 3 

sort -k3,1 -r chromosome_3_joined_maize.txt > increasing_chromosome_3_joined_maize.txt                      
 #this code sorts the file in increasing chromosome position in column 3
sed ’s/-t/?/‘ increasing_chromosome_3_joined_maize.txt  > encoded_increasing_chromosome_3_joined_maize.txt 
‘’’
#File type 1 chromosome 4 maize
‘’’
awk '$2 == 4’ joined_maize.txt  > chromosome_4_joined_maize.txt                                             
 #this code uses awk to select rows that contain chromosome 4 

sort -k3,1 -r chromosome_4_joined_maize.txt > increasing_chromosome_4_joined_maize.txt                      
 #this code sorts the file in increasing chromosome position in column 3
sed ’s/-t/?/‘ increasing_chromosome_4_joined_maize.txt  > encoded_increasing_chromosome_4_joined_maize.txtt  
‘’’
#File type 1 chromosome 5 maize
‘’’
awk '$2 == 5’ joined_maize.txt  > chromosome_5_joined_maize.txt                                              
#this code uses awk to select rows that contain chromosome 5

sort -k3,1  -r chromosome_5_joined_maize.txt > increasing_chromosome_5_joined_maize.txt                       
#this code sorts the file in increasing chromosome position in column 3
sed ’s/-t/?/‘ increasing_chromosome_5_joined_maize.txt  > encoded_increasing_chromosome_5_joined_maize.txt 
‘’’
#File type 1 chromosome 6 maize
‘’’
awk '$2 == 6’ joined_maize.txt  > chromosome_6_joined_maize.txt                                              
#this code uses awk to select rows that contain chromosome 6

sort -k3,1 -r  chromosome_6_joined_maize.txt > increasing_chromosome_6_joined_maize.txt                      
 #this code sorts the file in increasing chromosome position in column 3
sed ’s/-t/?/‘ increasing_chromosome_6_joined_maize.txt  > encoded_increasing_chromosome_6_joined_maize.txtt 
‘’’
#File type 1 chromosome 7 maize
‘’’
awk '$2 == 7’ joined_maize.txt  > chromosome_7_joined_maize.txt                                              
#this code uses awk to select rows that contain chromosome 7

sort -k3,1 -r chromosome_7_joined_maize.txt > increasing_chromosome_7_joined_maize.txt                       
#this code sorts the file in increasing chromosome position in column 3
sed ’s/-t/?/‘ increasing_chromosome_7_joined_maize.txt  > encoded_increasing_chromosome_7_joined_maize.txt
‘’’
#File type 1 chromosome 8 maize
‘’’
awk '$2 == 8’ joined_maize.txt  > chromosome_8_joined_maize.txt                                             
 #this code uses awk to select rows that contain chromosome 8

sort -k3,1  chromosome_8_joined_maize.txt > increasing_chromosome_8_joined_maize.txt                       
#this code sorts the file in increasing chromosome position in column 3
sed ’s/-t/?/‘ increasing_chromosome_8_joined_maize.txt  > encoded_increasing_chromosome_8_joined_maize.txt 
‘’’
#File type 1 chromosome 9 maize
‘’’
awk '$2 == 9’ joined_maize.txt  > chromosome_9_joined_maize.txt                                             
 #this code uses awk to select rows that contain chromosome 9

sort -k3,1 -r chromosome_9_joined_maize.txt > increasing_chromosome_9_joined_maize.txt                       
#this code sorts the file in increasing chromosome position in column 3
sed ’s/-t/?/‘ increasing_chromosome_9_joined_maize.txt  > encoded_increasing_chromosome_9_joined_maize.txt
‘’’
#File type 1 chromosome 10 maize
‘’’
awk '$2 == 10’ joined_maize.txt  > chromosome_10_joined_maize.txt                                              
#this code uses awk to select rows that contain chromosome 10

sort -k3,1 -r chromosome_10_joined_maize.txt > increasing_chromosome_10_joined_maize.txt                      
 #this code sorts the file in increasing chromosome position in column 3
sed ’s/-t/?/‘ increasing_chromosome_10_joined_maize.txt  > encoded_increasing_chromosome_10_joined_maize.txt 
‘’’


#File type 2 chromosome 1 maize
‘’’
awk '$2 == 1' joined_maize.txt  > chromosome_1_joined_maize.txt                                              
#this code uses awk to select rows that contain chromosome 3 

sort -k3,1  chromosome_1_joined_maize.txt > decreasing_chromosome_1_joined_maize.txt                      
 #this code sorts the file in decreasing chromosome position in column 3
sed ’s/-t/-/‘ decreasing_chromosome_1_joined_maize.txt  > encoded_decreasing_chromosome_1_joined_maize.txt 
‘’’
#File type 2 chromosome 2 maize
‘’’

awk '$2 == 2’ joined_maize.txt  > chromosome_2_joined_maize.txt                                              
#this code uses awk to select rows that contain chromosome 3 

sort -k3,1  chromosome_2_joined_maize.txt > decreasing_chromosome_2_joined_maize.txt                      
 #this code sorts the file in decreasing chromosome position in column 3
sed ’s/-t/-/‘ decreasing_chromosome_2_joined_maize.txt  > encoded_decreasing_chromosome_2_joined_maize.txt
‘’’
#File type 2 chromosome 3 maize
‘’’
sed ’s/-t/-/‘ decreasing_chromosome_1_joined_maize.txt  > encoded_decreasing_chromosome_1_joined_maize.txt                                           
#this code uses awk to select rows that contain chromosome 3 

sort -k3,1  chromosome_3_joined_maize.txt > decreasing_chromosome_3_joined_maize.txt                       
#this code sorts the file in decreasing chromosome position in column 3
sed ’s/-t/?/‘ decreasing_chromosome_3_joined_maize.txt  > encoded_decreasing_chromosome_3_joined_maize.txt
‘’’
#File type 2 chromosome 4 maize
‘’’
awk '$2 == 4’ joined_maize.txt  > chromosome_4_joined_maize.txt                                              
#this code uses awk to select rows that contain chromosome 4 

sort -k3,1  chromosome_4_joined_maize.txt > decreasing_chromosome_4_joined_maize.txt                       
#this code sorts the file in decreasing chromosome position in column 3
sed ’s/-t/-/‘ decreasing_chromosome_4_joined_maize.txt  > encoded_decreasing_chromosome_4_joined_maize.txt 
‘’’
#File type 2 chromosome 5 maize
‘’’
awk '$2 == 5’ joined_maize.txt  > chromosome_5_joined_maize.txt                                              
#this code uses awk to select rows that contain chromosome 5

sort -k3,1  chromosome_5_joined_maize.txt > decreasing_chromosome_5_joined_maize.txt                      
 #this code sorts the file in decreasing chromosome position in column 3
sed ’s/-t/-/‘ decreasing_chromosome_5_joined_maize.txt  > encoded_decreasing_chromosome_5_joined_maize.txt
‘’’
#File type 2 chromosome 6 maize
awk '$2 == 6’ joined_maize.txt  > chromosome_6_joined_maize.txt                                              
#this code uses awk to select rows that contain chromosome 6

sort -k3,1  chromosome_6_joined_maize.txt > decreasing_chromosome_6_joined_maize.txt                       
#this code sorts the file in decreasing chromosome position in column 3
sed ’s/-t/-/‘ decreasing_chromosome_6_joined_maize.txt  > encoded_decreasing_chromosome_6_joined_maize.txt

#File type 2 chromosome 7 maize
‘’’
awk '$2 == 7’ joined_maize.txt  > chromosome_7_joined_maize.txt                                              
#this code uses awk to select rows that contain chromosome 7

sort -k3,1  chromosome_7_joined_maize.txt > decreasing_chromosome_7_joined_maize.txt                      
 #this code sorts the file in decreasing  chromosome position in column 3
sed ’s/-t/-/‘ decreasing_chromosome_7_joined_maize.txt  > encoded_decreasing_chromosome_7_joined_maize.txt 
‘’’
#File type 2 chromosome 8 maize
‘’’
awk '$2 == 8’ joined_maize.txt  > chromosome_6_joined_maize.txt                                              
#this code uses awk to select rows that contain chromosome 8

sort -k3,1  chromosome_8_joined_maize.txt > decreasing_chromosome_8_joined_maize.txt                       
#this code sorts the file in decreasing chromosome position in column 3
sed ’s/-t/-/‘ decreasing_chromosome_8_joined_maize.txt  > encoded_decreasing_chromosome_8_joined_maize.txt
‘’’
#File type 2 chromosome 9 maize
‘’’
awk '$2 == 9’ joined_maize.txt  > chromosome_6_joined_maize.txt                                             
 #this code uses awk to select rows that contain chromosome 9

sort -k3,1  chromosome_9_joined_maize.txt > decreasing_chromosome_9_joined_maize.txt                      
 #this code sorts the file in decreasing chromosome position in column 3
sed ’s/-t/-/‘ decreasing_chromosome_9_joined_maize.txt  > encoded_decreasing_chromosome_9_joined_maize.txt
‘’’
#File type 2 chromosome 10 maize
‘’’
awk '$2 == 10’ joined_maize.txt  > chromosome_10_joined_maize.txt                                             
 #this code uses awk to select rows that contain chromosome 10

sort -k3,1  chromosome_10_joined_maize.txt > decreasing_chromosome_10_joined_maize.txt                       
#this code sorts the file in decreasing chromosome position in column 3
sed ’s/-t/-/‘ decreasing_chromosome_10_joined_maize.txt  > encoded_decreasing_chromosome_10_joined_maize.txt 
‘’’
## For Teosinte

#File type 1 chromosome 1 teosinte
awk '$2 == 1' joined_teosinte.txt  > chromosome_1_joined_teosinte.txt                                           
   #this code uses awk to select rows that contain chromosome 1 

sort -k3,1 -r chromosome_1_joined_teosinte.txt > increasing_chromosome_1_joined_teosinte.txt                      
 #this code sorts the file in increasing chromosome position in column 3
sed ’s/-t/-/‘ increasing_chromosome_1_joined_teosinte.txt  > encoded_increasing_chromosome_1_joined_teosinte.txt
‘’’
#File type 1 chromosome 2 teosinte
‘’’
awk '$2 == 2’ joined_teosinte.txt  > chromosome_2_joined_teosinte.txt                                             
 #this code uses awk to select rows that contain chromosome 2 


sort -k3,1 -r chromosome_2_joined_teosinte.txt > increasing_chromosome_2_joined_teosinte.txt                      
 #this code sorts the file in increasing chromosome position in column 3
sed ’s/-t/-/‘ increasing_chromosome_2_joined_teosinte.txt  > encoded_increasing_chromosome_2_joined_teosinte.txt 
‘’’
#File type 1 chromosome 3 teosinte
‘’’
awk '$2 == 3’ joined_teosinte.txt  > chromosome_3_joined_teosinte.txt                                            
  #this code uses awk to select rows that contain chromosome 3 

sort -k3,1 -r chromosome_3_joined_teosinte.txt > increasing_chromosome_3_joined_teosinte.txt                      
 #this code sorts the file in increasing chromosome position in column 3
sed ’s/-t/-/‘ increasing_chromosome_2_joined_teosinte.txt  > encoded_increasing_chromosome_2_joined_teosinte.txt
‘’’
#File type 1 chromosome 4 teosinte
‘’’
awk '$2 == 4’ joined_teosinte.txt  > chromosome_4_joined_teosinte.txt                                             
 #this code uses awk to select rows that contain chromosome 4 

sort -k3,1 -r chromosome_4_joined_teosinte.txt > increasing_chromosome_4_joined_teosinte.txt                      
 #this code sorts the file in increasing chromosome position in column 3
sed ’s/-t/-/‘ increasing_chromosome_4_joined_teosinte.txt  > encoded_increasing_chromosome_4_joined_teosinte.txt
‘’’
#File type 1 chromosome 5 teosinte
‘’’
awk '$2 == 5’ joined_teosinte.txt  > chromosome_5_joined_teosinte.txt                                             
 #this code uses awk to select rows that contain chromosome 5 

sort -k3,1 -r chromosome_5_joined_teosinte.txt > increasing_chromosome_5_joined_teosinte.txt                      
 #this code sorts the file in increasing chromosome position in column 3
sed ’s/-t/-/‘ increasing_chromosome_5_joined_teosinte.txt  > encoded_increasing_chromosome_5_joined_teosinte.txt
‘’’
#File type 1 chromosome 6 teosinte
‘’’
awk '$2 == 6’ joined_teosinte.txt  > chromosome_6_joined_teosinte.txt                                              
#this code uses awk to select rows that contain chromosome 6 

sort -k3,1 -r chromosome_2_joined_teosinte.txt > increasing_chromosome_2_joined_teosinte.txt                      
 #this code sorts the file in increasing chromosome position in column 3
sed ’s/-t/-/‘ increasing_chromosome_6_joined_teosinte.txt  > encoded_increasing_chromosome_6_joined_teosinte.txt
‘’’
#File type 1 chromosome 7 teosinte
‘’’
awk '$2 == 7’ joined_teosinte.txt  > chromosome_7_joined_teosinte.txt                                             
 #this code uses awk to select rows that contain chromosome 7 

sort -k3,1 -r chromosome_7_joined_teosinte.txt > increasing_chromosome_7_joined_teosinte.txt                       
#this code sorts the file in increasing chromosome position in column 3
sed ’s/-t/-/‘ increasing_chromosome_7_joined_teosinte.txt  > encoded_increasing_chromosome_7_joined_teosinte.txt
‘’’
#File type 1 chromosome 8 teosinte

awk '$2 == 8’ joined_teosinte.txt  > chromosome_8_joined_teosinte.txt                                              
#this code uses awk to select rows that contain chromosome 8 

sort -k3,1 -r chromosome_8_joined_teosinte.txt > increasing_chromosome_8_joined_teosinte.txt                       
#this code sorts the file in increasing chromosome position in column 3
sed ’s/-t/-/‘ increasing_chromosome_8_joined_teosinte.txt  > encoded_increasing_chromosome_8_joined_teosinte.txt

#File type 1 chromosome 9 teosinte
awk '$2 == 9’ joined_teosinte.txt  > chromosome_9_joined_teosinte.txt                                              
#this code uses awk to select rows that contain chromosome 9 

sort -k3,1 -r chromosome_9_joined_teosinte.txt > increasing_chromosome_9_joined_teosinte.txt                       
#this code sorts the file in increasing chromosome position in column 3
sed ’s/-t/-/‘ increasing_chromosome_9_joined_teosinte.txt  > encoded_increasing_chromosome_9_joined_teosinte.txt

#File type 1 chromosome 10 teosinte
awk '$2 == 10’ joined_teosinte.txt  > chromosome_10_joined_teosinte.txt                                              
#this code uses awk to select rows that contain chromosome 10 

sort -k3,1 -r chromosome_10_joined_teosinte.txt > increasing_chromosome_10_joined_teosinte.txt                       
#this code sorts the file in increasing chromosome position in column 3
sed ’s/-t/-/‘ increasing_chromosome_10_joined_teosinte.txt  > encoded_increasing_chromosome_10_joined_teosinte.txt

#File type 2 chromosome 1 teosinte


awk '$2 == 1' joined_teosinte.txt  > chromosome_1_joined_teosinte.txt                                             
 #this code uses awk to select rows that contain chromosome 1 

sort -k3,1  chromosome_1_joined_teosinte.txt > decreasing_chromosome_1_joined_teosinte.txt                       
#this code sorts the file in decreasing chromosome position in column 3
sed ’s/-t/-/‘ decreasing_chromosome_1_joined_teosinte.txt  > encoded_decreasing_chromosome_1_joined_teosinte.txt

#File type 2 chromosome 2 teosinte
‘’’
awk '$2 == 2’ joined_teosinte.txt  > chromosome_2_joined_teosinte.txt                                             
 #this code uses awk to select rows that contain chromosome 2 

sort -k3,1  chromosome_2_joined_teosinte.txt > decreasing_chromosome_2_joined_teosinte.txt                       
#this code sorts the file in decreasing chromosome position in column 3
sed ’s/-t/-/‘ decreasing_chromosome_2_joined_teosinte.txt  > encoded_decreasing_chromosome_2_joined_teosinte.txt
‘’’
#File type 2 chromosome 3 teosinte
‘’’
awk '$2 == 3’ joined_teosinte.txt  > chromosome_3_joined_teosinte.txt                                             
 #this code uses awk to select rows that contain chromosome 3 

sort -k3,1  chromosome_3_joined_teosinte.txt > decreasing_chromosome_3_joined_teosinte.txt                      
 #this code sorts the file in decreasing chromosome position in column 3
sed ’s/-t/-/‘ decreasing_chromosome_3_joined_teosinte.txt  > encoded_decreasing_chromosome_3_joined_teosinte.txt
‘’’
#File type 2 chromosome 4 teosinte
‘’’
awk '$2 == 4’ joined_teosinte.txt  > chromosome_4_joined_teosinte.txt                                              
#this code uses awk to select rows that contain chromosome 4 

sort -k3,1  chromosome_4_joined_teosinte.txt > decreasing_chromosome_4_joined_teosinte.txt                       
#this code sorts the file in decreasing chromosome position in column 3
awk -F, ‘“ “ == ?’ increasing_chromosome_1_snp_position.txt
‘’’
#File type 2 chromosome 5 teosinte
‘’’
awk '$2 == 5’ joined_teosinte.txt  > chromosome_5_joined_teosinte.txt                          
 #this cs awk to select rows that contain chromosome 5 

sort -k3,1  chromosome_5_joined_teosinte.txt > decreasing_chromosome_5_joined_teosinte.txt                   
    #this code sorts the file in descreasing chromosome position in column 3
sed ’s/-t/-/‘ decreasing_chromosome_5_joined_teosinte.txt  > encoded_decreasing_chromosome_5_joined_teosinte.txt
‘’’
#File type 2 chromosome 6 teosinte
‘’’
awk '$2 == 6’ joined_teosinte.txt  > chromosome_6_joined_teosinte.txt                                             
 #this code uses awk to select rows that contain chromosome 6 

sort -k3,1  chromosome_6_joined_teosinte.txt > decreasing_chromosome_6_joined_teosinte.txt                      
 #this code sorts the file in decreasing  chromosome position in column 3
sed ’s/-t/-/‘ decreasing_chromosome_6_joined_teosinte.txt  > encoded_decreasing_chromosome_6_joined_teosinte.txt
‘’’
#File type 2 chromosome 7 teosinte
‘’’
awk '$2 == 7’ joined_teosinte.txt  > chromosome_7_joined_teosinte.txt                                           
   #this code uses awk to select rows that contain chromosome 7 

sort -k3,1  chromosome_7_joined_teosinte.txt > decreasing_chromosome_7_joined_teosinte.txt                       
#this code sorts the file in decreasing chromosome position in column 3
sed ’s/-t/-/‘ decreasing_chromosome_7_joined_teosinte.txt  > encoded_decreasing_chromosome_7_joined_teosinte.txt
‘’’
#File type 2 chromosome 8 teosinte
‘’’
awk '$2 == 8’ joined_teosinte.txt  > chromosome_2_joined_teosinte.txt                                               

sort -k3,1  chromosome_8_joined_teosinte.txt > decreasing_chromosome_8_joined_teosinte.txt                       
#this code sorts the file in decreasing chromosome position in column 3
sed ’s/-t/-/‘ decreasing_chromosome_8_joined_teosinte.txt  > encoded_decreasing_chromosome_8_joined_teosinte.txt
‘’’
#this code uses awk to select rows that contain chromosome 8
#File type 2 chromosome 9 teosinte
‘’’
awk '$2 == 9’ joined_teosinte.txt  > chromosome_9_joined_teosinte.txt                                             
 #this code uses awk to select rows that contain chromosome 9 

sort -k3,1  chromosome_9_joined_teosinte.txt > decreasing_chromosome_9_joined_teosinte.txt                       
#this code sorts the file in decreasing chromosome position in column 3
sed ’s/-t/-/‘ decreasing_chromosome_9_joined_teosinte.txt  > encoded_decreasing_chromosome_9_joined_teosinte.txt
‘’’
#File type 2 chromosome 10 teosinte
‘’’
awk '$2 == 10’ joined_teosinte.txt  > chromosome_10_joined_teosinte.txt                                             
 #this code uses awk to select rows that contain chromosome 10 

sort -k3,1  chromosome_10_joined_teosinte.txt > decreasing_chromosome_10_joined_teosinte.txt                       
#this code sorts the file in decreasing chromosome position in column 3
sed ’s/-t/-/‘ decreasing_chromosome_10_joined_teosinte.txt  > encoded_decreasing_chromosome_10_joined_teosinte.txt
‘’’
File type 3 maize
‘’’
awk '$3 ~ /unknown/' joined_maize.txt > unknown_joined_maize.txt 
‘’’
#using awk this selects the lines that contain the unknown value in the third column for position and turns it into a new file.  

File type 3 teosinte 

‘’’
awk '$3 ~ /unknown/' joined_teosinte.txt > unknown_joined_teosinte.txt 
‘’’
#using awk this selects the lines that contain the unknown value in the third column for position and turns it into a new file.  


