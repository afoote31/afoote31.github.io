---
layout: distill
title: Intellectual Property and Infectious Disease Treatment in Developing Nations
date: 2026-07-31 12:00:00
featured: false
description: The role of international IP in access to treatment for 1990s AIDS and present-day tuberculosis
tags: 
categories:
pretty_table: true
mermaid:
  enabled: true
  zoomable: true
code_diff: true
map: true
chart:
  chartjs: true
  echarts: true
  vega_lite: true
tikzjax: true
typograms: true

authors:
  - name: Aaron Foote
    affiliations:
      name: UC Berkeley
giscus_comments: true
bibliography: 2018-12-22-distill.bib

---

**This is a topic that I am actively learning more about, so if you have an insight, comment, or critique on what I present here, please leave it as a comment at the bottom!**

In the US, AIDS was thought of as a gay disease, but it also spread rapidly through blood bank negligence<d-cite key="BloodBankBook"></d-cite><d-cite key="bloodBankRuling"></d-cite>, users of injected drugs, and heterosexual sex <d-footnote>I highly recommend *And the Band Played On* by Randy Shilts <d-cite key="shilts"></d-cite> for an account of AIDS in the US.</d-footnote>. Africa did not associate AIDS with homosexuality, as the disease spread through heterosexual intercourse, mother-to-child transmission, and injections/transfusions. By the end of 1997, around 30.5 million people lived with AIDS, with 21 million of them residing in Sub-Saharan Africa<d-cite key="unaids1998"></d-cite>. In developed countries, blood screening had been enforced, AZT treatment was given to mothers and newborns during/after pregnancy to reduce vertical transmission, and highly active antiretroviral therapy changed HIV from a death sentence to a manageable disease. However, these prevention/treatment tools were not widely available in Africa simply because the drugs were not affordable. In this post, I explore the role that international intellectual property played in preventing access to life-saving drugs for AIDS.

**There needs to be a bit on TB here. Something like "It is much the same today..." and then give a sentence or two on how things have changed (generally), how the same candidate solutions have the same hurdles, and what is the current state.** That'll be the end of the intro.

### The TRIPS Agreement

In the early 1990s, the binding force in international trade was the General Agreement on Tariffs and Trade (GATT). However, this agreement proved insufficient for a developing world economy, and lacked enforcement power. Thus, in 1995, the World Trade Organization was founded through the extension of GATT and the reimagining of member responsibilities and enforcement mechanisms. During the same negotiations, the Agreement on Trade-Related Aspects of Intellectual Property Rights (TRIPS) was signed, laying out the foundation upon which today's international IP law is built.

International protection of IP was a concept brought to the US government by about a dozen corporate executives who banded together to form the Intellectual Property Committee. Their effectiveness at organizing amongst themselves and alongside their European and Japanese counterparts was essential to their success in turning their vision for international intellectual property into law<d-cite key="Mizruchi"></d-cite>, and their access to experts in intellectual property law relative to other parties gave them a considerable leg up in negotiations<d-cite key="pppl"></d-cite> of TRIPS. 

Fundamentally, stakeholders in developed nations wanted tighter intellectual property restrictions in developing nations along with policies that gave those restrictions teeth, while developing nations wanted to continue to protect their fledgling domestic industries. Two of the more controversial strategies used by developing countries were compulsory licensing and parallel importation. Through compulsory licensing, a government grants a license to a company to produce a product patented by a different company (e.g. an African country giving a domestic manufacturer the license to produce an HIV antiretroviral treatment). A country that engages in parallel importation purchases a patented product from a party that produced the product other than the patent holder (e.g. an African country importing HIV antiretroviral treatments from India rather than from a US manufacturer).

In TRIPS, pharmaceutical industries were able to get legislation included to enforce data exclusivity. While not directly blocking companies from developing generic treatment alternatives, Article [39](https://www.wto.org/english/docs_e/legal_e/27-trips_04d_e.htm) allows patent holders to block other companies from using their clinical trial data in order to assist in the approval of a generic alternative. There is certainly support for such a provision<d-cite key="dataExclusivity"></d-cite>, but this measure kills nearly any attempt at generic drug development before it can even begin, since companies are forced to essentially replicate findings that have already been established through trials funded in large part by the government. 

Other articles give developing nations ground to stand on to argue protective policies they have in place. For instance, Article [8](https://www.wto.org/english/res_e/publications_e/ai17_e/trips_art8_jur.pdf) granted member nations the right to "adopt measures necessary to protect public health and nutrition... provided that such measures are consistent with the provisions of this Agreement". The wording leaves the interpretation up to the states regarding protection, although it does mention consistency with the TRIPS Agreement, creating ambiguity. Article [31](https://www.wto.org/english/docs_e/legal_e/27-trips_04c_e.htm) pertains to compulsory licensing. As with the other articles, it gives a lot of room for interpretation to member nations. However, only a member nation can grant a compulsory license. Additionally, before doing so, the potential licensee must have reasonably tried to negotiation with the license holder. This reasonable negotiation can be waived by the member nation if there is a national emergency. The member nation must pay "adequate remuneration" to the license holder, which is hard to calculate. It is pointed out that article (f), stating "any such use shall be authorized predominantly for the supply of the domestic market of the Member authorizing such use" leaves ambiguous whether the member nation granting the compulsory license must manufacture the product domestically or if they're allowed to import it<d-cite key="leis"></d-cite>. Finally, TRIPS specifically leaves the issue of parallel importation up to the member nations. 

### USTR and the Special 301 Mechanism
Section 182 of the Trade Act of 1974 requires the Office of the United States Trade Representative to conduct an annual review to identify countries abusing intellectual property rights or denying fair market access to American goods. US companies and IP holders can submit complaints for review, but the complaints can only be about other governments violating their IP, not other companies. Between 1996 and 2000, most of the requests have been submitted by pharmaceutical companies<d-cite key="pppl"></d-cite>. Countries that fail the review process can be placed into three categories:

##### Watch List
This is the least severe category. This is for countries with weak enforcement of IP, barriers to market access, or gaps in their laws that don’t meet international standards, but are still generally cooperative with the US. The 2024 report included Algeria, Barbados, Belarus, Bolivia, Brazil, Bulgaria, Canada, Colombia, Ecuador, Egypts, Guatemala, Mexico, Pakistan, Paraguay, Peru, Thailand, Trinidad and Tobago, Turkey, Turkmenistan, and Vietnam<d-cite key="specialReport2024"></d-cite>.

##### Priority Watch List
You end up in this category if you have more severe and longstanding IP issues, a lack of progress on implementing policy, or minimal to no cooperation in dialogue with the US. In 2024, this category included Argentina, Chile, China, India, Indonesia, Russia, and Venezuela<d-cite key="specialReport2024"></d-cite>.

##### Priority Foreign Country
This is for the most severe IP offenders, and countries are rarely put into this category. This is for nations for which IP violations are the most severe, are clearly government-enabled, and show no sign of slowing down. In 2024, no countries were placed into this category<d-cite key="specialReport2024"></d-cite>.

At the time of this post's writing, the Trump is using this mechanism to levy tariffs on [many countries](https://www.whitehouse.gov/presidential-actions/2026/07/actions-by-the-united-states-in-the-investigations-under-section-301-of-the-trade-act-of-1974-of-the-acts-policies-and-practices-of-60-economies-related-to-the-failure-of-each-economy-to-impose-and/). This practice is [not expected](https://www.piie.com/blogs/realtime-economics/2026/why-trump-will-lose-again-new-challenge-his-tariffs) to hold up in court.

Consequences of being placed on these lists include sanctions, increased tariffs (the Trump strategy), or being taken to international court. It has been criticized for effectively being a tool for corporations to force the US government to use its power to enforce corporate IP preferences across the world. For instance, under TRIPS, compulsory licensing is allowed. However, in practice, when countries try to issue compulsory licenses to get access to treatments to harrowing diseases like AIDS, the USTR steps in and punishes them<d-cite key="Vick"></d-cite>.

## South Africa and SAMRSA

In 1997, the South African government passed the South African Medicines and Related Substances Act, granting the Minister of Health broad powers regarding intellectual property for medicine in South Africa. The goal of the act was to make affordable medication available to protect public health, which was necessary in a year that saw 700,000 South Africans become infected with HIV<d-cite key="unaids1998"></d-cite>. However, there was swift pushback internationally, as pharmaceutical companies felt that this act violated TRIPS. In particular, Section 15c allowed the South African Minister of Health, in order to protect public health, to decide that the rights of a patent holder cannot be acted upon. This prevented companies from going to court to have their patents enforced. Additionally, Section 22c gives the Minister of Health the power to grant licenses to manufacture, sell, import, export or distribute medicines or medical devices. Notably, the manufacturer/distributor need not be domestic<d-cite key="leis"></d-cite>.

A critic concerned with the compliance of this act with international law would point to Sections 15c and 22c. The broad powers granted to the South African government by this law are argued to conflict with the TRIPS agreement. They point to section 15c failing to explicitly require adequate compensation and good faith negotiations, and that section 15c(b) gives South Africa the power to issue compulsory licenses to foreign nations. Critics believe that SAMRSA oversteps by delving into international trade, while article 31f of TRIPs states “any such use shall be authorized predominantly for the supply of the domestic market of the Member authorizing such use”. A counter would be that some countries are unable to produce the drug themselves, and thus are acting within their rights as respondents to an emergency by granting these compulsory licenses.

In response to the Act, 39 members of the Pharmaceutical Manufacturers of South Africa filed a lawsuit to take South Africa to international court. Additionally, the Pharmaceutical Research and Manufacturers of America (PhRMA) successfully pressured the US government to get South Africa placed on the 301 Watch List, and later put additional pressure by getting further trade benefits removed. 

Recognizing that the US government had a large role in pressuring South Africa to repeal legislation that had the potential to save thousands of lives, activists got involved to pressure the government to separate itself some pharma agendas. They focused on Al Gore, vice president under Clinton and soon-to-be future presidential candidate, disrupting his live televised rallies with banner, chants, and noisemakers. The protests were highly effective. The same week that Gore declared his candidacy for president, the Clinton administration walked back their policies pressuring South Africa<d-cite key="pppl"></d-cite>. This reversal indicated a larger switch in policy from the Clinton administration. The following year, an executive order was passed prohibiting the USTR from targeting sub-Saharan African countries for legislation passed to increase access to HIV/AIDS treatment. Thus, the protests were successful in getting the US government to act against the wishes of pharmaceutical companies, assisting sub-Saharan Africa to obtain and maintain access to affordable HIV/AIDS treatment. The lawsuit against South Africa is another case of activists successfully thwarting pharmaceutical industry desires to put profit over lives. Pressure from academic researchers who originally discovered the antiretroviral treatments, protests with images of dying mothers and babies, and coordinated research showing that drug manufacturing prices were far lower than what companies professed created enough public pressure that the companies ended up withdrawing their lawsuit altogether just one day into the trial<d-cite key="halbert"></d-cite>.

While there was still much work to be done, intellectual property and AIDS in the late 1990s is an instance where activists were able to enact meaningful change to save lives, defeating an industry with far more legal and financial firepower.

# TB in the present day
