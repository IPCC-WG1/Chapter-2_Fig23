##########################################################################
# ---------------------------------------------------------------------------------------------------------------------
# This is [Matlab]* code to produce IPCC AR6 WGI Figure/s [Panel b of figure 2.23 or figure 2.23b] *
# Creator: [Lucas Ruiz]*, [IANIGLA, CONICET, Argentina] 
# Contact: [lruiz@mendoza-conicet.gob.ar]*
# Last updated on: [06]* [28]*, [2021]* (e.g., March 1st, 2021)
# --------------------------------------------------------------------------------------------------------------------
#
# - Code functionality: [Script to generate the  annual and decadal global glacier mass change (Gt yr-1) from 1961 until 2018 for Figure 2.23.b. Includes the global annual mass balance from Zemp et al. (2019/2020), global mass balance between 2002-2016 from Wouters et al. (2019), global mass balance between 2006-2015 from SROCC and decadal (2000-2010 and 2010-2020) global mass balance from Hugonnet et al. (2021). To run the script "MB_figure_FGD_chapter2_jun_28_2021.m" you will need:
 'Zemp_etal_results_global.csv'
 'table_hugonnet_regions_10yr_ar6period.xlsx'
 'shadedplot.m' matlab function
 'colorscheme.mat' created by the TSU of WGI] *

# - Input data: ['Zemp_etal_results_global.csv' supplementary materials from Zemp, M., Huss, M., Thibert, E., Eckert, N., McNabb, R., Huber, J., et al. (2019). Global glacier mass changes and their contributions to sea-level rise from 1961 to 2016. Nature 568, 382–386. doi:10.1038/s41586-019-1071-0.
 'table_hugonnet_regions_10yr_ar6period.xlsx' Table made by Romain Hugonnet for Chapter 9 from the data published in Hugonnet, R., McNabb, R., Berthier, E., Menounos, B., Nuth, C., Girod, L., et al. (2021). Accelerated global glacier mass loss in the early twenty-first century. Nature 592, 726–731. doi:10.1038/s41586-021-03436-z.]*

# - Output variables: [pane_b/black line. Zemp_etal_results_global.csv. Global mass change (Gt yr-1) based on spatial interpolation from 1961 to 2016; supplementary materials from Zemp et al. (2019)  it is complemented with the mass change for years 2017 and 2018 from Table 1 of Zemp et al. (2020). Decadal means are computed by the matlab script. Panel_b/grey area. Zemp_etal_results_global.csv. Total uncertainty of regional mass change (Gt yr-1) from 1961 to 2016; supplementary materials from Zemp et al. (2019) it is complemented with the uncertainty of mass change for years 2017 and 2018 from Table 1 of Zemp et al. (2020). Decadal uncertainties are computed by the matlab script. Panel_b/blue line. Global mean glacier mass balance (Gt yr-1) between 2002 and 2016 from Wouters et al. (2019). Values are taken from Table 1 of Wouters et al. (2019) Global total of glacier mass budget. Values are declared in the matlab script.
panel_b/light blue area. Global mean glacier mass balance uncertainty (Gt yr-1) between 2002 and 2016 from Wouters et al. (2019). Values are taken from Table 1 of Wouters et al. (2019) Global total of glacier mass budget uncertainty. Values are declared in the matlab script. Panel_b/desert yellow line. Global mean glacier mass balance (Gt yr-1) between 2006 and 2015 from Hock et al. (2019) Values are taken from Table 2A.1 of Chapter 2 of SROCC Global values. Values are declared in the matlab script. Panel_b/desert yellow area. Global mean glacier mass balance uncertainty (Gt yr-1) between 2006 and 2015 from Hock et al. (2019) Values are taken from Table 2A.1 of Chapter 2 of SROCC Global values. Values are declared in the matlab script.
panel_b/green line. table_hugonnet_regions_10yr_ar6period.xlsx. Decadal (2000-2010 and 2010-2020) global mass balance (Gt yr-1)  from Hugonnet et al. (2021). The mean values are computed in the matlab script from the value of each region. Panel_b/green area. table_hugonnet_regions_10yr_ar6period.xlsx. Decadal (2000-2010 and 2010-2020) global mass balance (Gt yr-1)  uncertainty from Hugonnet et al. (2021). The mean values are computed in the matlab script from the value of each region. 
Reference to the original datasets.
Hock, R., Rasul, G., Adler, C., Cáceres, B., Gruber, S., Hirabayashi, Y., et al. (2019). “High Mountain Areas,” in IPCC Special Report on the Ocean and Cryosphere in a Changing Climate, eds. H.-O. Pörtner, D. C. Roberts, V. Masson-Delmotte, P. Zhai, M. Tignor, E. Poloczanska, et al. (In Press), 131–202. Available at: https://www.ipcc.ch/srocc/chapter/chapter-2.
Hugonnet, R., McNabb, R., Berthier, E., Menounos, B., Nuth, C., Girod, L., et al. (2021). Accelerated global glacier mass loss in the early twenty-first century. Nature 592, 726–731. doi:10.1038/s41586-021-03436-z.
Zemp, M., Huss, M., Eckert, N., Thibert, E., Paul, F., Nussbaumer, S. U., et al. (2020). Brief communication: Ad hoc estimation of glacier contributions to sea-level rise from the latest glaciological observations. Cryosph. 14, 1043–1050. doi:10.5194/tc-14-1043-2020.
Zemp, M., Huss, M., Thibert, E., Eckert, N., McNabb, R., Huber, J., et al. (2019). Global glacier mass changes and their contributions to sea-level rise from 1961 to 2016. Nature 568, 382–386. doi:10.1038/s41586-019-1071-0.]
#
# ----------------------------------------------------------------------------------------------------
# Information on  the software used
# - Software Version: [MatlabR2013]*
# - Landing page to access the software: [if possible provide a DOI]* 
# - Operating System: [Windows10 ]*
# - Environment required to compile and run: [Matlab ]*
#  ----------------------------------------------------------------------------------------------------
#
#  License: Apache 2.0
#
# ----------------------------------------------------------------------------------------------------
# How to cite:
Gulev, S.K., P.W. Thorne, J. Ahn, F.J. Dentener, C.M. Domingues, S. Gerland, D. Gong, D.S. Kaufman, H.C. Nnamchi, J. Quaas, J.A. Rivera, S. Sathyendranath, S.L. Smith, B. Trewin, K. von Schuckmann, and R.S. Vose, 2021: Changing State of the Climate System. In Climate Change 2021: The Physical Science Basis. Contribution of Working Group I to the Sixth Assessment Report of the Intergovernmental Panel on Climate Change[Masson-Delmotte, V., P. Zhai, A. Pirani, S.L. Connors, C. Péan, S. Berger, N. Caud, Y. Chen, L. Goldfarb, M.I. Gomis, M. Huang, K. Leitzell, E. Lonnoy, J.B.R. Matthews, T.K. Maycock, T. Waterfield, O. Yelekçi, R. Yu, and B. Zhou (eds.)]. Cambridge University Press, Cambridge, United Kingdom and New York, NY, USA, pp. 287–422, doi:10.1017/9781009157896.004.

# When citing this code, please include both the code citation and the following citation for the related report component:
  https://doi.org/10.5281/zenodo.6328226


########################################################################




Am keeping this for reference:
# ----------------------------------------------------------------------------------------------
# Acknowledgement: The template for this file was created by Lina E. Sitz (https://orcid.org/0000-0002-6333-4986), Paula A. Martinez (https://orcid.org/0000-0002-8990-1985), and J. B. Robin Matthews (https://orcid.org//0000-0002-6016-7596)
