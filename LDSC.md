import seaborn as sb
import seaborn as sb
import seaborn as sb
import seaborn as sb

df = pd.read_csv("C:\\Users\\e620470\\001 AUTOMATION PROJECTS\\LDSC\\Output\\df_final_adv_data.csv", delimiter = "|", index_col=0)
df["CPTY_ID"] = pd.to_numeric(df["COUNTERPARTY_NEW"])*1
df["NTG_AGR_REF"]= df["NETTING_AGREEMENT_REFERENCE"]
df

df_unet= df.loc[(df['NETTING_AGREEMENT_REFERENCE'].isnull()) & (df['Product'] == 'FX')] #**Unnetted Transactions**#
df_net = df.loc[(df['NETTING_AGREEMENT_REFERENCE'] != None) & (df['Product'] == 'FX')]  #**Netted Transactions**#

df_unet["CPTY_ID"] = pd.to_numeric(df_unet["COUNTERPARTY_NEW"])*1
df_net["CPTY_ID"] = pd.to_numeric(df_net["COUNTERPARTY_NEW"])*1

df_net["FAIR_VALUE"]= pd.to_numeric(df_net["FAIR_VALUE"])
df_unet["FAIR_VALUE"]= pd.to_numeric(df_unet["FAIR_VALUE"])
df_net["CE"]= pd.to_numeric(df_net["CE"])
df_unet["CE"]= pd.to_numeric(df_unet["CE"])

df_net["NGR"] = df_net["FAIR_VALUE"]//df_net["CE"]
df_net["NGR"].fillna(0, inplace=True)

df_unet["NGR"] = df_unet["FAIR_VALUE"]//df_unet["CE"]
df_unet["NGR"].fillna(0, inplace=True)
