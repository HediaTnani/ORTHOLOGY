# ORTHOLOGY

'''
def pathways (organism):
  import requests
  import json
  import pandas as pd
  import re
  pathwaylist = []
  kegg_url =  "http://rest.kegg.jp/list/pathway/" 
  pathwayslist = kegg_url + organism
  response = requests.get(pathwayslist)
  response.text.split("\n")
  current_section = None
  for line in response.text.split("\n"):
    #print(line)
    if not line == "":
        m = re.search("path:([\w\d]+)\s+(.+)\s+-\s*\w+", line)
        if m:
            pathwaylist.append(m.group(1))
  return pathwaylist
  '''
  '''
  def pathway2genes (lmalist):
    import requests
    import json
    import pandas as pd
    import re
    genlist = []
    organism = lmalist[0][:3]
    for i in range(len(lmalist)):
      pathway = lmalist[i]
      print("==========" +lmalist[i] + "===============")
      kegg_url =  "http://rest.kegg.jp/get/" 
      pathwayurl = kegg_url + pathway
      response = requests.get(pathwayurl)
      response.text.split("\n")
      current_section = None
      for line in response.text.split("\n"):
          #print(line)
          section = line[:12].strip()
          #print(line[:12].strip())
          if not section == "":
              current_section = section
              #print(current_section)
          if current_section == "GENE":
              right_column = line[12:]
              #print(right_column)
              #genes = right_column[12:]
              #print(genes)
              m = re.search("(.+?)\s+(.+)", right_column)
              if m:
                  #print(m.group(1))
                  genlist.append({'PATHWAY':pathway, 'GENE_ID':m.group(1)})


    result = pd.DataFrame(genlist)
    #print(result)
    result.to_csv('./'+organism + '_Pathwaysgenelist.csv', index=False, header=None)
    return result
    '''
