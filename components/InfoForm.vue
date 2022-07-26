<template>
  <form :class="{'theme-red': theme == 'red'}" class="px-12 py-5 pb-16 space-y-4">
    <div>
      <label for="major">Permanent ZIP</label>
      <input v-model="studentInfo['Permanent ZIP']" type="text">
    </div>
    <div>
      <label for="gpa">GPA</label>
      <div class="flex space-x-6 items-center">
        <input v-model="studentInfo['GPA']" type="text" class="!w-[100px] text-center" :class="{'!w-[200px]': theme == 'red'}" />
        <div class="controls flex space-x-5 items-center">
          <button
            aria-label="plus-0.1"
            class="flex items-center justify-center bg-white p-[.35em] rounded-full w-6 h-6 shadow-md"
            @click.prevent="studentInfo['GPA'] = studentInfo['GPA'] + 0.1"
          >
            <!-- <img src="~/assets/imgs/icons/plus-blue.svg" alt="" /> -->
            <svg xmlns="http://www.w3.org/2000/svg" width="50" viewBox="0 0 22.769 22.769"><path d="M22.769 11.384a1.751 1.751 0 0 1-1.751 1.752h-7.882v7.881a1.751 1.751 0 0 1-3.5 0v-7.881H1.751a1.751 1.751 0 0 1 0-3.5h7.881V1.752a1.751 1.751 0 1 1 3.5 0v7.881h7.881a1.749 1.749 0 0 1 1.756 1.751Z"/></svg>
          </button>
          <button
            aria-label="minus-0.1"
            class="flex items-center justify-center bg-white p-[.35em] rounded-full w-6 h-6 shadow-md"
            @click.prevent="studentInfo['GPA'] = studentInfo['GPA'] - 0.1"
          >
            <svg xmlns="http://www.w3.org/2000/svg" width="20" viewBox="0 0 26 4"><rect width="26" height="4" rx="2"/></svg>
            <!-- <img src="~/assets/imgs/icons/minus-blue.svg" width="20" alt="" /> -->
          </button>
        </div>
      </div>
    </div>
    <div>
      <label for="major">ACT Score</label>
      <input v-model="studentInfo['ACT Comp']" type="text">
    </div>
    <div v-for="(value, propertyName) of dataValues">
      <label :for="propertyName">{{ propertyName }}</label>
      <select v-model="studentInfo[propertyName]" :id="propertyName" name="major" id="major">
        <option value="">Choose</option>
        <option :value="item" v-for="item of value.sort()">{{ item }}</option>
      </select>
    </div>
    <div v-if="theme == 'red'" class="pt-12 pb-6">
      <button @click.prevent="$emit('predict', studentInfo)" class="flex rounded-xl w-full py-1 px-6 text-center items-center justify-center space-x-5 font-semibold text-[1.4rem] font-sans" style="box-shadow: 0px 8px 15px #00000029;">
        <span>Go</span>
        <img src="~assets/imgs/rocket.png" width="35" alt="">
      </button>
    </div>
  </form>
</template>

<script>
export default {
  props: ['theme'],
  data() {
    return {
      dataValues: {
        "College Code Branch": [
          '001528-00', '001989-00', '001817-00', '006961-00', '009917-00',
          '007691-00', '001991-00', '002002-00', '005244-00', '001979-00',
          '038193-00', '006960-00', '001999-00', '001990-00', '005273-00',
          '026236-00', '003273-00', '009942-00', '001162-00', '009275-00',
          '001807-00', '003530-00', '002471-00', '001365-00', '002001-00',
          '030838-00', '008849-00', '001077-00', '007115-00', '003486-00',
          '001996-00', '005271-00', '001081-00', '001701-00', '001993-00',
          '004586-00', '001977-00', '020530-00', '001843-00', '003677-00',
          '003745-00', '030345-00', '003119-00', '007191-00', '003223-00',
          '001153-00', '002025-00', '008677-00', '001958-00', '001809-00',
          '001976-00', '030357-00', '001334-00', '001982-00', '001954-00',
          '001586-00', '003078-00', '007694-00', '001827-00', '003371-00',
          '001489-00', '001825-00', '001961-00', '002580-00', '002105-00',
          '002328-00', '001808-00', '003240-00', '003125-00', '002503-00',
          '001881-00', '001801-00', '003483-00', '002565-00', '025083-00',
          '001083-00', '001370-00', '003018-00', '002054-00', '003090-04',
          '005304-00', '001960-00', '007933-00', '001795-00', '001108-00',
          '007118-00', '001648-00', '009767-00', '001051-00', '004852-00',
          '002957-00', '001813-00', '004027-00', '003077-00', '001692-00',
          '001504-00', '003068-00', '001470-00', '006982-00', '003402-00',
          '001013-00', '003090-00', '003478-00', '008145-00', '001536-00',
          '003954-00', '006911-00', '001786-00', '001747-00', '001737-00',
          '041301-00', '042118-00', '003549-01', '003523-00', '002058-00',
          '020739-00', '001574-06', '001948-00', '003329-00', '002173-00',
          '010362-00', '011644-00', '001710-00', '009841-00', '002927-00',
          '004003-00', '003170-00', '002243-00', '003510-00'
        ],
        "Enrollment Major": [
          'GENERAL STUDIES(PER ENRICHMENT)',
          'NUTR & FD SCI-HOSPITALITY MGT & TOUR',
          'MERCHANDISING APPAREL AND TEXTILES', 'NURSING-PRE (RN-BSN) BSN',
          'COMMUNICATION ARTS TECHNOLOGY', 'UNDECIDED TRANSFER',
          'COMPUTER INFORMATION SYSTEMS', 'INDUSTRIAL TECHNOLOGY',
          'BUSINESS ADMINISTRATION', 'UNDECIDED BUSINESS BSB',
          'HEALTHCARE SPEC RESP THER INT', 'UNDECIDED BACCALAUREATE',
          'HEALTH CARE SUPPORT-NURSING IN', 'ASSOCIATE IN SCIENCE',
          'Undeclared', 'ASSOCIATE IN ARTS', 'UNDERGRADUATE STUDIES',
          'ACCOUNTING', 'CRIMINAL JUSTICE', 'UNDECIDED',
          'ELEMENTARY EDUCATION', 'BUS MANAGEMENT & MARKETING',
          'COMPUTER AND INFORMATION TECHNOLOGIES', 'INTERNATIONAL STUDIES',
          'GENERAL BUSINESS', 'PRE-FINANCE', 'EDUCATION', 'PRE-MANAGEMENT',
          'RELIGION', 'YOUTH CARE WORK', 'APPRENTICE TECH ELECTRICIAN',
          'HEALTHCARE SPEC RN INTEREST', 'MIDDLE & SEC ED/UNDECIDED - BS',
          'BUSINESS BSB', 'JUSTICE ADMINISTRATION-BS', 'UNDECLARED',
          'AUCTIONEERING', 'COMPUTER AND INFORMATION TECH',
          'SOCIAL SCIENCES', 'PRE-BIOLOGY BA',
          'DIGITAL GAME SIMULATION DESIGN', 'COURSES ONLY',
          'ADMINISTRATION OF JUSTICE AS T', 'UNDECLARED IN AS (BA)',
          'EQUINE STUDIES', 'AVIATION MAINTENANCE TECHNOLOG',
          'ADVANCED BUSINESS ADMIN', 'MANAGEMENT',
          'SMALL BUSINESS MANAGEMENT',
          'COMPUTER INFORMATION TECHNOLOGY MAJOR', 'EXERCISE SCIENCE MAJOR',
          'APPRENTICE TECH PLUMB PIPE', 'SELECTED COURSES', 'ACCOUNTANCY',
          'NOT APPLICABLE', 'MARKETING', 'AAS BUSINESS',
          'ACCOUNTANCY BSB/INFORMAT SECTY', 'LIMITED RADIOGRAPHER',
          'PHYS THERAPIST ASSISTANT', 'PRE-BUSINESS BSB', 'NURSING SCIENCE',
          'FINANCE PRE-MAJOR', 'ACCOUNTING PRE-MAJOR',
          'FMCS:TEXTILES & APPAREL CONC', 'ELECTRONICS',
          'BUSINESS ECON (SEEKING ADM)', 'APPRENTICE TECH:(ELECTRICIAN)',
          'PRE NURSING', 'ACCOUNTING TRAINEE I', 'FINANCE',
          'PRE-SECONDARY EDUCATION BSED', 'JUSTICE ADMINISTRATION',
          'COMPUTER INFORMATION TECH-PREP', 'PRE-ACCOUNTING',
          'COMMUNICATION - BA', 'BUSINESS ECONOMICS', 'BUSINESS TRANSFER',
          'TRANSFER COURSE ENROLLEE', 'PROGRAMMING', 'NETWORK SECURITY',
          'ROUTING AND SWITCHING', 'COMPUTER INFO SYS/INFO SECUR',
          'DENTAL HYGIENE (INT) PENDING', 'INFORMATION TECHNOLOGY',
          'ECONOMICS - BA', 'HEALTH CARE FOUNDATIONS- BASIC',
          'UNDECLARED IN BN (BS)', 'ENGLISH',
          'UNDECLARED-NON-DEGREE SEEKING', 'FIRE SCIENCE TECHNOLOGY',
          'SPORT ADMIN - BS', 'TELEVISION PRODUCTION', 'JOURNALISM MAJOR',
          'EQUINE ADMINISTRATION', 'MIDDLE & SEC ED/SST - BS',
          'UNDECLARED IN UNIVERSITY STUDIES (BA)', 'IT GAMING DESIGN',
          'APP TEC ABC ELECTRICAL CONC', 'ARTS & SCIENCES UNDECLARED',
          'CATERING & PERSONAL CHEF', 'BS IN COMPR ENGR & COMP SCI',
          'PERSONAL INTEREST', 'PRE-BUSINESS', 'PRE-COMMUNICATION BA',
          'AVIATION MAINTENANCE TECH', 'ELECTRICAL ENGINEERING',
          'PSYCHOLOGY-BA', 'HIGH SCHOOL DUAL ENROLL',
          'PRE BUSINESS ADMINISTRATION', 'CHEMISTRY W/BUSINESS TRACK',
          'COMPUTER INFO SYS/WEB DEVELOP', 'ORG LDRSHIP AND L/HEALTHLE-SET',
          'PRE-ENGINEERING', 'CHEMISTRY -BA P', 'POTENTIAL ATS', 'BIOLOGY',
          'EXPLORATORY BACCALAUREATE', 'EARLY ELEM ED/ENGC - BSR',
          'MATHEMATICS - BS P', 'ENTREPRENEURSHIP', 'MARKETING SEEKING ADM',
          'BSN IN NURSING (C)', 'KINESIOLOGY CSU TRANSFER',
          'GENERAL OCCUPATIONAL AND TECHNICAL STUDIES', 'DUAL ENROLLMENT',
          'ART - BA', 'FINANCE SEEKING ADM',
          'ANTHROPOLOGY/NATURAL SCI TRACK', 'HEALTH SCIENCE TECHNOLOGY',
          'UNSPECIFIED - NFA', 'RULE 10/HIGH SCHOOL',
          'ACCOUNTING SEEKING ADM', 'NFA-PSYCHOLOGY',
          'COMPUTER GRAPHICS TECH', 'ART/ COMM ART & DESIGN-BFA',
          'SOCIAL WORK - INTENDED', 'CIVIL ENGINEERING',
          'COMPUTER ENGINEERING', 'EXPLORATORY UNDECLARED',
          'INDUSTRIAL ENGINEERING', 'POLITICAL SCIENCE', 'CRIMINOLOGY',
          'EARLY ELEM ED/MATH - BSR', 'MUSIC EDUCATIONBMEINSTRUMENT',
          'BOYCE WHITEFIELD ACADEMY STUDENT', 'BACHELOR OF ARTS IN FRENCH',
          'PSYCHOLOGY/ SOCIAL SCIENCE', 'INDIVIDUALIZED MAJOR',
          'FINANCE BSB', 'PRE-PSYCHOLOGY BS', 'ECONOMICS MAJOR',
          'COMMUNICATION - BS', 'PUBLIC HEALTH BA',
          'HUMANITIES SOC SCI NON DEG', 'HIGH SCHOOL PROGRAM',
          'MECHANICAL ENGINEERING', 'GENERAL STUDIES-COLLEGE W/H.S.',
          'EXPLORATORY', 'LIBERAL ARTS', 'BUSINESS INFORMATION SYSTEMS',
          'ELECTRICAL TECHNOLOGY', 'FINANCE PRE-MAJOR (BSBA)', 'VIOLA',
          'EARLY ELEM ED/UNDECIDED - BSR', 'GENERAL STUDIES',
          'INDUSTRIAL MAINTENANCE TECHNICIAN', 'HLTH&HUMPERF/EXERSCI - BS',
          'MUSIC BM/INSTRUMENTAL PERFORMA', 'DENTAL HYGIENE (LL) - BS',
          'COMPUTER INFO SYS/BUS PROC MAN', 'COMPUTER INFO SYS - INTENDED',
          'AASA-BA', 'GENERAL STUDIES-GUEST', 'PSYCHOLOGY-BS',
          'CHEMISTRY - BS P', 'BS IN BUSINESS ADMINISTRATION',
          'DUAL ENROLLMENT WHITEFIELD ACADEMY',
          'AVIATION MAINTENANCE TECHNOLOGY', 'PRE-NURSING',
          'INDUSTRIAL MAINTENANCE TECHNOLOGY',
          'POLITICAL SCIENCE/GLOBAL&INTER', 'ART - BA P',
          'BUSINESS ECON SEEKING ADM', 'HISTORY/TRACK-SOCIAL SCIENCES',
          'BUS', 'ASSOCIATE OF GENERAL STUDIES', 'ASSOCIATE OF ARTS',
          'ANIMAL SCIENCE', 'NON-DEG JOB/PERSONAL IMPROV',
          'CONTINUING EDUCATION',
          'DUAL ENROLLMENT CHRISTIAN EDUCATION CONSORTIUM',
          'BIOLOGY/ CELLULAR/ PHYSIOL-BS', 'BIOENGINEERING-BACH OF SCIENCE',
          'PRE SPORTS MANAGEMENT BSTESM', 'HISTORY', 'BUSINESS MANAGEMENT',
          'GEOGRAPHY/GEOG GEOSP TECH', 'COMPUTER MANUFACTURING & MACHINING',
          'UNIVERSITY STUDIES', 'CHEMISTRY BS/BIOCHEMISTRY TRAC',
          'FINANCIAL PERSPECTIVES', 'COMPUTER SCIENCE BS', 'TRANSIENT',
          'GENERAL', 'ACCOUNTANCY - ONLINE', 'BUS ADMIN FINANCE',
          'PRE-SOCIAL WORK', 'PRE-EDUCATION', 'SPORT INDUSTRY',
          'BUSINESS ADMINISTRATION TRANSF', 'COMPUTER INFO SYSTEMS',
          'BIOLOGY/ECOLOGY-BS', 'ENGLISH - PROF AND PUBLIC WRIT',
          'BUSINESS ADMINISTRATION-ONLINE', 'BS IN COMPR SCI & ENGR',
          'BS: BUSINESS ADMINISTRATION', 'CHEMICAL ENGINEERING', 'BUSINESS',
          'GEOGRAPHY/METEOROLOGY-BS', 'SUPPLY CHAIN MANAGEMENT',
          'ASIAN STUDIES', 'POLS SCIR/BS/LAW & PUBL POL',
          'MANAGEMENT SEEKING ADM', 'GENERAL STUDIES - INTG',
          'BIOLOGY / MOLECELLDEVELOP', 'PRE-COMPUTER SCIENCE BS',
          'PRE-INFORMATICS BS', 'HUMANITIES / FILM STUDIES', 'MARKETING BSB',
          'BIOLOGY - BA', 'INFORMATICS BS', 'LATIN AMERICAN&LATINO STUDIES',
          'THEATRE ARTS - BS', 'GENERAL TRANSFER STUDIES', 'PRE-ECONOMICS',
          'CHEMISTRY-AS', 'CIT-SOFTWARE-AAS',
          'ADV FOOD & BEVERAGE MANAGEMENT', 'FILMMAKING: SCRIPT TO SCREEN',
          'ELECTRONIC MEDIA AND BROADCASTING MAJOR',
          'EQUINE SCIENCE AND MANAGEMENT', 'BUSINESS ADMIN',
          'JAPANESE LANGUAGE AND LITERATURE', 'ACCOUNTING/FINANCE',
          'PRE MGMT/MANAGEMENT', 'MARKETING (SEEKING ADM)',
          'CONSTRUCTION MANAGEMENT', 'ACCT', 'PUBLIC HEALTH BS',
          'MUSIC/BM/JAZZ PERFORMANCE', 'SPORT MANAGEMENT',
          'SPORTS BUSINESS PRE-MAJOR', 'MUSIC THERAPY - BM',
          'GENERAL STUDIES BGS-ONLINE', 'POLYSOMNOGRAPHY',
          'MEDICAID NURSE AIDE', 'PRE-PUBLIC HEALTH', 'MUSIC OTHER',
          'EARLY ELEM ED/ELBD - BSR', 'ENGINEERING TECHNOLOGY',
          'ENGINEERING', 'INFORMATION SECURITY', 'ZOO ANIMAL TECHNICIAN',
          'POLITICAL SCIENCE/LAW&PUB POL', 'SOCIOLOGY - BS P',
          'MUSIC BA/MUSIC AND NEW MEDIA', 'NEUROSCIENCE - BS',
          'PRE-NURSING BSN', 'GAME ART AND DEVELOPMENT', 'ED',
          'INTERDISCIPLINARY EARLY CHILDHOOD EDUCATION',
          'PRE-BUSINESS - ONLINE', 'CYBER SECURITY INFO ASSURANCE',
          'HISTORY / TRACK IN HUMANITIES', 'RECORDING INDUSTRY'
        ],
        "College State": [
          'FL', 'KY', 'IN', 'IL', 'WV', 'AZ', 'PA', 'OH', 'CA', 'TN', 'MO',
          'CO', 'VA', 'UT', 'OR', 'LA', 'GA', 'NH', 'MD', 'MI', 'NE', 'ME',
          'WI', 'AR', 'AL', 'NC', 'CT', 'RI', 'ID', 'TX', 'KS', 'MA', 'NV',
          'OK',
        ],
        "Scholarship": [
          'National Scholars Program', 'KEES Scholarship Fall',
       'Distance Educ-Communications', 'KEES Scholarship Spring',
       'Sub Direct Stafford Loan', 'Unsub Direct Stafford Loan',
       'Est MC-UPS Grade Reimb-Fall', 'MC Grade Reimb. (Y0008) NF',
       'UPS Grade Reimb. (Y0008) NF', 'Est MC-UPS Grade Reimb-Spring',
       'Outside Loan', '1st Yr Acad Comp Grant 2010-11',
       'Pell Grant 1 2010-2011', 'Rechter Family Scholarship',
       'No Fin-Aid', 'Outside Scholarship', 'Wimsett Scholarship',
       'Cap Grant Fall', 'Direct Subsidized Loan', 'Pell Grant 2017-2018',
       'SEOG Grant 2017-2018', 'Need Based Financial Aid',
       'Cap Grant Spring', 'Federal Direct Unsub Loan',
       'Federal Pell Grant Additional', 'Federal Direct Subsidized Loan',
       'Federal Pell Grant 2018-2019', 'Federal SEOG Grant 2018-2019',
       'Federal Pell Grant 2019-2020', 'Federal SEOG Grant 2019-2020',
       'SEOG Grant 2010-2011', 'W. R. Porter, Sr. Scholarship',
       'SEOG Grant 2011-2012', 'Pell Grant 1 2011-2012',
       'Pell Grant 2012-2013', 'SEOG Grant 2012-2013',
       'Pell Grant 2013-2014', 'SEOG Grant 2013-2014',
       'Pell Grant 2014-2015', 'SEOG Grant 2014-2015',
       'Direct Unsubsidized Loan', 'Direct Grad/Prof PLUS Loan',
       'BKD,LLP Scholarship', 'Alumni Association Sch',
       'Harold Adams Scholarship', 'OFE-Heuser Sch Business',
       'Trustees First Year Sch.', 'Trustees Acad Scholarship',
       'Entrepreneur Res Prize', 'Pell Grant 2015-2016',
       'SEOG Grant 2015-2016', 'Porter Full Tuition Scholarshi',
       'Direct Parent PLUS Loan', 'University Grant',
       'Federal Work Study 2011-2012', 'McBride Scholarship',
       'Jones Student Travel Fund (2)', 'MC Grade Reimb. (Y0008) ALL',
       'Est. Metropolitan College', 'Outside Scholarship-NF',
       'Academic Commonwealth Sch', 'Estimated Housing Benefit',
       'Outside Scholarship(2)-NF', 'QFE-Bus/Acctg Ernst Young',
       'Alumni Future Leader Sch', 'JOHN E BROWN SCHOLARSHIP FUND',
       'Ollie Green Jr Award', 'Bryant Scholarship',
       'Ath Sch-Women-Swimming-Board', 'Ath Sch-Women-Swimming-Room',
       'Athletic Books', 'Athletics-Women-Swimming',
       'Summer & 5th Year Aid-Tuition', 'Athletic Sch-Rowing-Tuition',
       'CIS Scholastic Excellence Sch', 'Student Govt Assoc-No Future',
       'Student Senate', 'Cardinal Covenant', 'Assessment',
       'Wire Payment-Veterans 33', 'Third Party Auth-VA33-T&O',
       'Transfer Scholarships', 'Federal Perkins Loan',
       'Athletics-Men-Baseball', 'Stu-Athlete Opportunity Fund',
       'Ath Sch-Men-Baseball-Books', 'Football Sch-Manager GA',
       'Pell Grant 2016-2017', '2014 Idea State U Business Pla',
       'COB Entrepreneurship Program', 'KY Equine Indstry Pari-Mutual',
       'Athletics-Women-Soccer', 'Ath Sch-Women-Soccer-Books',
       'Ath Sch-Men-Baseball-Room', 'Federal Work Study 2012-2013',
       'UPS Grade Reimb. (Y0008)ALL', 'Charles Denny Scholarship',
       'Hilliard J H - State', 'Freshman First Year Initiative',
       'Alternative Loan (EFT Payment)', 'Potential Outside Scholarship',
       'Porter Full Tuition Sch', 'COB Grad Scholarships',
       'Bonnie Thornton Scholarship', 'Federal Work Study 2013-2014',
       'Shampain Scholarship', 'Federal Direct PLUS Loan',
       'SEOG Grant 2016-2017', 'GLBA Business Plan Competition',
       'Federal Work Study 2014-2015', 'BKD Scholarship Endowment (T&O',
       'Federal Work Study 2015-2016', 'Student Support Services (NF)',
       'Jerry/Karen Borowick Sch', 'J C Bowling Scholarship',
       'TR-F/S Dependent (IRS)', 'KY Equine Administration',
       'Gifts-Bus. Scholarship Alumni', 'Rechter Family Sch II',
       'Ath Sch-Men-Swimming-Board', 'Ath sch-Men-Swimming-Room',
       'Athletics-Men-Swimming', 'Grief Scholarship',
       'Crowe-Chizek Scholarship', 'Institute of Internal Auditors',
       'TR-F/S Dependent', 'TR-Employee (UG)', 'Credit for Credits',
       'J Burns Scholarship', 'Buck Marshall Scholarship',
       'Jones Scholars Fund II', 'Scoppechio Rise Above Scholshp',
       'Federal HEERF Grant 20-21', 'MORTON WALKER SCHOLARSHIP FUND',
       'Strickler Memorial Fund', 'Curtin Family Fund',
       'Payment - Third Party', 'Commonwealth Student Support',
       'KEES Scholarship Fall 2018/19', 'KEES Scholarship Sprg 2018/19',
       'RA-Housing', 'Overseer Mentor Program',
       'Summer Tuition Scholarship', 'SP 2022 Fed HEERF Grant 21-22',
       'National City Fellowship', 'Spd-Inspire', 'FTMBA Tuition-COB',
       'Nardelli scholarship', 'R Charles Moyer Scholrshp Fund',
       'Mass Aid Fund (NF)', 'Denny Crum Scholarship',
       'Marching Band Sch-NF', 'Ky Equine Industry Pari-Mutuel',
       'Winnia Scholarship', 'A&S Speech Course Pack',
       "Women's & Gender Studies", '2014 Student Persistence Fund',
       'QFE-Modern Languages', 'Federal SEOG Grant 2020-2021',
       'Federal Pell Grant 2020-2021', 'CAP Grant Fall 2020',
       'Federal HEERF Grant 21-22', 'Zorn Scholarship Fund',
       'McBride Scholarship Gift', 'Ford/EEOC Scholarship',
       'Stone family Scholarship', 'J H Hilliard Fund',
       'Modern Languages Endowment', 'RICHARD & CONSTANCE LEWIS END',
       'Shell Unit-Stud Aid', 'C B P A Scholarship',
       'A&S Army ROTC Scholarship', 'J B Speed Trust Fund Scholarsh',
       'Army ROTC-NF', 'Wire Payment/Army-AF ROTC',
       'Rodney Williams Scholarship', 'ARMY ROTC CC Paymt',
       'Outside Scholarship(2)-Tuition', 'Third Party Auth - Tuition',
       'Third Party Auth - Tuit & Opt', 'Watkins Finance Scholarship',
       'Summer-Ath TR-Men-Basketball', 'Summer-Men-Basketball Sch-Room',
       'Athletic Sch-Men-Basketball', 'Cheerleader Scholarship',
       'Management Sch-Community', 'Eddie Morris Fund',
       'Stamm Scholarship-Economics', 'Economics',
       'Henry Vogt Scholarship', 'MLK-Peace Award', 'Ky National Guard',
       "Women's Golf-Tuition", "Women's Golf-Room", "Women's Golf-Board",
       'W Golf Room On Campus', 'Ollie Green Tax  Award',
       'Fall Alternative Loan (EFT)', 'Spring Alternative Loan (EFT)',
       'Football Sch-Manager-Equipment', 'Football Scholarship-Books',
       'Dept Award-Check', 'Federal Work Study 2016-2017',
       'Federal Work Study 2017-2018', 'Minority Recruitment',
       'FM Strickler Endowed', 'Jones Scholarship-State Match',
       'Summer-Ath Sch-Women-BB-Board', 'Summer-Ath Sch-Women-BB-Room',
       'Summer-Ath TR-Women-Basketball', 'Ath Sch-Women-Basketball-Board',
       'Ath Sch-Women-Basketball-Room', 'Athletic Board',
       'Athletics-Women-Basketball', 'W BASKETBALL MISC EXP GAP',
       'Est. Athletic Room', 'T/R DSA - BPA',
       'David & Betty Jones Scholars', 'KY Coal County Schp (KCCCCS)',
       'Vivian Hill Scholarship', 'Outside Scholarship on Check',
       'A A T P Award', 'Equine Education Improvements',
       'BKD LLP Scholarship Gift', 'Athletics-Women-Field Hockey',
       'Ath-Women-Field Hockey-Books', 'Ath Sch-Women-Hockey-Board',
       'Ath-Women-Field Hockey-Room', 'Intramurals Misc',
       'McConnell Sch-Political Lead', 'Athletic TR-Lacrosse',
       'Lacrosse-Books', 'CAP Grant Spring 2021',
       'Federal Pell Grant 2021-2022', 'CAP Grant Spring 2022',
       'Athletic Sch-Rowing-Board', 'Athletic Sch-Rowing-Room',
       'ROWING MISC EXP GAP', 'Athletic Sch-Rowing-Books',
       'Potential Athletic SAOF', 'W Rowing Room On Campus',
       'Federal Direct ParentPLUS Loan', 'John H. Schnatter Center',
       'Lacrosse-Room', 'LACROSSE MISC EXP GAP', 'Lacrosse-Board',
       '2018 Idea State U Business', 'Athletics-Men-Soccer',
       'Non-Resident State Grant Prog.', 'Ath Sch-Men-Soccer-Board',
       'Ath Sch-Men-Soccer-Room', 'Birmingham Area Alumni Club',
       'Sum-Ath TR-Women-Volleyball', 'Summer-Women-Volleyball-Board',
       'Summer-Women-Volleyball-Room', 'Ath Sch-Women-Volleyball-Board',
       'Ath Sch-Women-Volleyball-Room', 'Athletics-Women-Volleyball',
       "Women's Volleyball-Books", 'VOLLEYBALL MISC EXP GAP',
       'Burks Scholarship', "Women's Softball-Tuition",
       'Softball Room OnCampus', "Women's Softball-Board",
       "Women's Softball-Room", 'Resident Education & Prog',
       'Pay It Forward Student Fund', 'Student Persistence Fund',
       'M Basketball SUM Room OnCamp', 'M Basketball Room On Campus',
       'Men Basketball-Brd On Camp', 'Rodney Williams Legacy Sch',
       'Est. Outside Loan', 'RSA & NRRH', 'Ferguson Travel Fund',
       'Rives International Fund', 'EFT Payment-Third Party',
       'Outside Scholarship(2)-NF-EFT', 'Federal Work Study 2018-2019',
       'CARES Act Emergency Fin Aid Gr', 'COB Honors Program',
       'KAPT PrePaid Payment', 'KEES Scholarship Fall 2019/20',
       'W GOLF MISC EXP GAP', "Ath Sch-Women's Golf-Books",
       'Lexington Area Alumni Sch', 'Athletics-Men-Tennis',
       'Ath Sch-Men-Tennis-Room', 'Ath Sch-Men-Tennis-Board',
       'Summer & 5th Year Aid-Board', "Men's Tennis-Books",
       'MACC Tuition COB Differential', 'Marketing Interns Sch-Board',
       'KEES Scholarship Sprg 2019/20', 'International Service Learning',
       'SPAD Program', 'Wm Bennett Scholarship (T&O)', 'Strickler Award',
       'Athletic Bands - (NF)', 'The College-to-Career Launch',
       'Panama QLU Program', "Lou Credit Men's Scholarship",
       'CIS General Scholarships', 'Torchbearer Endowment',
       'T/R State KRS 515', 'Athletics Sch-Men-Football',
       'FOOTBALL-MISC EXP GAP', 'Men-Football Sch-Board',
       'Men-Football Sch-Room', 'Summer-Athletics TR-Football',
       'Summer-Men-Football Sch-Board', 'Summer-Men-Football Sch-Room',
       'Political Science Department', 'SSC Federal HEERF Grnt 20-21',
       'Federal SEOG Grant 2021-2022', 'CAP Grant Fall 2021',
       'Summer & 5th Year Aid-Room', 'Ath Sch-Men-Baseball-Board',
       'Sports Medicine-Board', 'Harold Adams Sch-NF',
       'C S & Milah Lynn Scholarship', 'Chilton & Medley Scholarship',
       'Summer Alternative Loan (EFT)', 'COB Student Council',
       'Athletics-Men-Track', "Men's Track-Books",
       '2015 Student Persistence Fund', 'Tampa/St Petersburg Alumni',
       'Tampa Bay Endowed Scholarship', 'Rowing-Brd On Camp',
       'Est. Misc Exp Gap', 'Athletic-Marketing-Books',
       'Athletic-Marketing-Room', 'MLK Scholars',
       'Muhammad Ali Scholarships', 'Muhammad Ali Institute',
       'Honors and MLK Support', "Women's Swimming-Books",
       'W Basketball Room OnCampus', 'W Basketball SUM Rm OnCampus',
       'M Soccer Room OnCampus', 'Ath Sch-Men-Soccer-Books',
       'M Tennis Room OnCampus', 'Athletics-Women-Tennis',
       'W TENNIS MISC EXP GAP', 'W Tennis Room OnCampus',
       'Ath Sch-Women-Tennis-Board', 'Summer-Women-Tennis-Room',
       'Summer-Women-Tennis-Board', 'Ath Sch-Women-Tennis-Room',
       'Summer-Ath TR-Women-Tennis', 'Summer-5th Year-Sch Board',
       "Women's Tennis-Books", 'M SWIMMING MISC EXP GAP',
       'Summer-Men-Basketball Sch-Boar', 'M BASKETBALL-MISC EXP GAP',
       'Men-Basketball Sch-Board', 'Men-Basketball Sch-Books',
       'Federal Perkins Summer Loan', 'Equipment - Ath TR',
       'Equipment Rm On Campus', 'Equipment - Brd On Camp (Sum)',
       'Equipment - Books', 'Athletics-Men-Golf', 'T/R State KRS 507',
       'Porter Scholarship', 'Martin Luther King Scholarship',
       'Payment-Americorps', 'LSAMP:KY-WV Mid-Level Alliance',
       'Louis Stokes STEM Pathways', 'T/R State KRS2847',
       'T/R State KRS 505', 'Disc funds - VP Std Af',
       'Student Emergency Fund', 'ROTC Scholarship',
       'A&S International Program', 'KEES Fall 20-21AY',
       'Drummond Scholarship', 'CFE-Charles Koch Foundation',
       'SPD-M. & F. Diebold Outreach', 'Welenken & Masters Scholarship',
       'KEES Spring 20-21AY', '2016 Student Persistence Fund',
       'Lindemeyer Acct Sch (17-18)', 'Meyer Accounting Scholarship',
       'Lewis Fund/Latin America', 'Rives Travel Fund-EBS Germany',
       "O'Neil Memorial Scholarship", 'Mountjoy & Bressler, LLP',
       'Federal Work Study Summer 2019', 'Football Sum Rm On Campus',
       'Football Room On Campus', 'BOA Emergency Fund',
       "Ath Sch-Men's Golf-Books", "Women's Softball-Books",
       'COB-Online MBA', 'SOFTBALL MISC EXP GAP',
       'Federal Work Study 2019-2020', 'M Swimming Room OnCampus',
       "Men's Swimming-Brd On Camp", 'TRANSFER NATIONAL SCHOLARS PRG',
       'Wm G Caldwell Scholarship', 'W Swimming Room OnCampus',
       'Ath TR-Winter', 'Bill Hartack Memorial Sch',
       'Warner L Jones, Jr. Memorial', 'George J Howe Fund',
       'Athletics TR-Equipment', 'Equipment - Board', 'Cardinal Pledge',
       'QFE-KURFEES AWARD', 'EWAB Scholarship', 'QFE-Scholarship-Acctg',
       'KEES Fall 21-22AY', 'Etscorn Scholar Fund',
       'Transdisciplinary Consortium-U', 'Outside Scholarship-TUITION',
       'Internationalization Act', 'Maxwell Spicker Jr Fund',
       'Rommel Johnson Scholarship', 'Ath Sch-Women-Soccer-Manager',
       'Potential KEES-Spring', '2017 Student Persistence Fund',
       'Womens Hockey-Brd On Camp', 'Winter-Ath TR-Field Hockey',
       'TRIO Student Support Services', 'Outside Scholarship-NF-EFT',
       'UL Healthcare Scholarship', 'Federal Work-Study 2020-2021',
       'EGSC (Early Graduation Schp)', 'Student Affairs Retention Fund',
       'HEERF Winter Session 21-22', 'Baseball Room On Campus',
       'Ray Glass Scholarship', 'Spr Alternative Loan Estimate',
       'Ath Sch-Women-Track-Board', 'Athletics-Women-Track',
       "Women's Track-Books", 'International Study Abroad',
       '2018 Student Persistence Fund', 'Cultural Center Student Prog',
       'AIDIDAS INTERN Aid-Board', 'Davidson, T&D-Endowed Fund',
       "Women's Track-Brd On Camp", '5th Year-Brd On Camp (Sum)',
       "Women's Track-Manager", 'Go Higher Grant', "Men's Swimming-Books",
       'UofL Grant', 'KY National Guard 19-20AY',
       'KY National Guard 20-21AY', 'KY National Guard 21-22AY',
       'Expected National Guard', 'A&S Air Force Scholarship',
       'Federal SEOG 20AY Emergency', 'Federal Work Study 2021-2022',
       'Baseball SUM Room OnCamp', 'Summer-Athletics TR-Baseball',
       'Student Government Assoc. Schl', 'BFP Tuition Scholarships',
       'BFP Enrichment Projects', 'Gardner Family Scholarship', 'K C P I',
       'Hispanic/Latino Initiatives', 'Strothman and Co Sch',
       'Gifts Equine Administration', 'SFAO Federal HEERF Grnt 21-22',
       'BASEBALL-MISC EXP GAP', 'Equine Scholarship',
       'Joel Goldstein Memorial', 'COMM Dept. Course Pack and Pub',
       'Denny Crum Scholarship-NF', 'Field Hockey SUM Room OnCampus',
       'Summer-Ath TR-Field Hockey', 'Lacrosse-Manager',
       'Summer-Ath TR-Women Soccer', 'Ath Sch-Women-Soccer-Room',
       'Ath Sch-Women-Soccer-Board', 'Ath Sch-Men-Baseball-Manager',
       'Est. Bookstore Scholarship', 'Federal SEOG 21AY Emergency',
       'SSC Federal HEERF Grnt 21-22', 'Volleyball SUM Room OnCampus',
       'Robert & Odile Whitaker Endowe', 'UofL Financial Aid Scholarship',
       'Summer-Ath TR Men-Soccer', 'International Student Fee',
       'Latino Success Fund', 'International Affairs',
       "Women's Tennis-Brd On Camp", '2019 Student Persistence Fund',
       '5th Year SUM Room On Camp', 'SFAO PJ Federal HEERF 21-22',
       'Music School Scholarship', 'Cardinal Academy',
       'Dorothy Norton Clay', 'PAUL SCHULTZ ENDOWED FUND',
       'Doris Bickel Charitable Fund', 'Geraldine Hamlet Fund',
       'SHPEP Summer 2021 Grant', 'Mordean Taylor Archer Schl.',
       '50th Anniversary Scholarship', 'Music-Pep Band Scholarship',
       "Women's Swimming-Brd On Camp", 'Football Sch-Manager -Video',
       'Women Basketball Board- On Cam', 'W Soccer SUM Room OnCamp',
       'Debate Team Scholarship', 'M Soccer SUM Room OnCamp',
       'Men Bball-Brd On Camp (Sum)', 'Kroger Scholars - Business',
       'Ulmer Family Scholarship', 'Panhellenic Leadership Sch.',
       'Orientation Program', 'Savannah Walker Memorial Schl.',
       'Guaranteed Transfer Scholarshi', 'Sagar Patagundi Scholarship',
       'COB Travel Fund Scholarship', 'Ath Sch-Men-Soccer-Manager',
       'Fields, Wh Memorial', 'Speed School Scholarship',
       'M TENNIS MISC EXP GAP', 'Mayer Fund', 'W Track Room OnCampus',
       'UGS High School Dual Credit TU', 'Ath Sch-Women-Track-Room',
       'Fall Alternative Loan Estimate', 'Fees Remitted-GA-VPSA',
       'M Golf Room On Campus', 'Mens Golf-Brd On Camp',
       'Steffond Johnson Memorial Scho', 'Womens Golf-Brd On Camp',
       'Cardinal Commitment', 'Inst HEERF REACH XCelerator',
       'Fifth Year SUM Room OnCampus', 'Volleyball Room OnCampus',
       'Outside Financial Assistance-N', 'Potential N-R State Grant',
       'Third Party Auth-VA 31-T&O', 'Wire Payment-Veterans 31',
       'Ath Sch-Women-Field Hockey-MGR', 'Mentoring Program Gifts',
       'Houston Alumni Schlr', 'Student Activity Center',
       'FIELD HOCKEY MISC EXP GAP', 'Outreach 9-12',
       'Vaughn M Stevens Scholarship', 'Carl F. Pollard Scholarship',
       'Carl F. Pollard Endowed Schsp', 'GO ARMY CC Paymt',
       'Summer-5th Year Sch-Room', 'Flexner Scholarship - Music',
       'Deans Disc Std Support', 'QFE-Music',
       'Bratcher CMBSpeed Scholarship', 'SPD- Kroger Zero Hunger Sch',
       'Federal Work Study Summer 2021', "Men's Tennis-Brd On Camp",
       'W Soccer Room OnCampus', 'Lacrosse Room On Campus',
       'Lacrosse-Brd On Camp', 'Ky Faculty/Staff Waiver (UG)',
       'Baseball Board-On Campus', 'Mens Soccer-Brd On Camp',
       'Summer-Ath TR-Women Golf'
        ],
        "Enrollment CIP": [
          '.', '520901', '190901', '513801', '100105', '500406', '0',
          '110101', '150612', '520201', '240102', '510711', '512601',
          '300101', '240101', '520302', '430103', '131202', '302001',
          '520801', '131501', '520101', '380201', '440701', '460302',
          '520301', '131206', '521901', '450101', '260101', '110803',
          '430107', '10507', '470608', '110103', '131314', '460502',
          '521401', '510907', '510806', '521201', '150000', '520601',
          '131205', '90101', '420101', '240104', '111003', '111002',
          '510602', '450601', '513902', '900000', '230101', '430203',
          '310504', '90701', '90401', '520299', '120503', '140901', '141001',
          '400501', '131320', '139999', '469999', '270101', '310505',
          '309999', '500702', '450201', '510000', '140801', '143501',
          '110401', '451001', '450401', '131312', '390604', '160901',
          '512201', '141901', '500903', '470303', '310501', '500901',
          '300000', '540101', '10901', '240199', '160301', '140501',
          '520903', '450701', '480503', '110701', '520701', '140701',
          '520203', '50103', '430104', '110104', '240103', '50107', '500501',
          '500602', '90402', '10307', '160302', '520305', '529999', '512305',
          '510917', '513901', '500999', '140102', '260701', '451101',
          '261501', '190709', '501003'
        ],
        "County": [
          'Out-of-State', 'Fayette County', 'Hardin County',
          'Jefferson County', 'Spencer County', 'Morgan County',
          'Edmonson County', 'Boyd County', 'Carter County', 'Oldham County',
          'Nelson County', 'Marion County', 'Barren County',
          'Anderson County', 'Warren County', 'Bullitt County',
          'McCracken County', 'Henry County', 'Kenton County',
          'Shelby County', 'Greenup County', 'Boone County', 'Boyle County',
          'Campbell County', 'Breckinridge County', 'Simpson County',
          'Washington County', 'Henderson County', 'Scott County',
          'Daviess County', 'Caldwell County', 'Carroll County',
          'Taylor County', 'Christian County', 'Lewis County',
          'Trigg County', 'Lincoln County', 'Franklin County',
          'Madison County', 'Ohio County', 'Woodford County',
          'Hancock County', 'Monroe County', 'Hopkins County',
          'Pulaski County', 'Owen County', 'Graves County', 'Hart County',
          'Calloway County', 'Bourbon County', 'Bell County',
          'Jessamine County', 'Meade County', 'Larue County',
          'Fleming County', 'Mason County', 'Letcher County',
          'Marshall County', 'Jackson County', 'Union County',
          'Trimble County', 'Clark County', 'Mercer County',
          'Livingston County', 'Grant County', 'Pike County',
          'Harrison County', 'Grayson County', 'McLean County',
          'Rowan County', 'Johnson County', 'Whitley County', 'Bath County',
          'Butler County', 'Clay County', 'Lawrence County', 'Lyon County',
          'Gallatin County', 'Breathitt County', 'Menifee County',
          'Knox County'
        ],
        "Student Group": [
          'None', 'ULTR', 'METR', 'ATCL', 'ATSW', 'ATIF', 'HONA', 'ATMA',
          'ATWS', 'ATBS', 'HONE', 'FGCS', 'ATSM', 'HONS', 'ATWT', 'ATFB',
          'ATDF', 'VETS', 'ATGF', 'ATWB', 'ATRF', 'ATFH', 'VT33', 'ATLX',
          'ATRM', 'ATMS', 'ATVB', 'ATOF', 'ATMT', 'ATPB', 'RECH', 'ATMG',
          'CHIL', 'V6', 'ATST', 'NSP3', 'ATMP', 'HONR', 'NSP6', 'ATPS',
          'DCVS', 'HONB', 'HONL', 'NSP5', 'ATMB', 'NSP4', 'NSPA', 'NSPB',
          'HONP', 'NSPD', 'NSP7', 'V33', 'HOS1'
        ],
        "Public Or Private": [
          'Public', 'Private'
        ],
        "Race": [
          'WHITE', 'BLACK', 'TWO OR MORE RACES', 'ASIAN', 'HISPANIC',
         'NATIVE HAWAIIAN OR OTHER PACIFIC ISLANDER', 'NON-RESIDENT ALIEN',
         'AMERICAN IND/ALASKAN NATIVE'
        ],
        "State": [
          'FLORIDA', 'KENTUCKY', 'INDIANA', 'ILLINOIS', 'NEW YORK',
         'ARIZONA', 'TENNESSEE', 'MISSOURI', 'HAWAII', 'MICHIGAN', 'IOWA',
         'VIRGINIA', 'MARYLAND', 'PENNSYLVANIA', 'NEW JERSEY',
         'MASSACHUSETTS', 'SOUTH CAROLINA', 'OHIO', 'GEORGIA',
         'SAUDI ARABIA', 'NORTH CAROLINA', 'TEXAS', 'COLORADO',
         'RHODE ISLAND', 'CONNECTICUT', 'ALABAMA', 'CALIFORNIA',
         'CZECH REPUBLIC', 'KOREA, REPUBLIC OF', 'KANSAS', 'ALASKA',
         'CHINA', 'SPAIN', 'SWAZILAND', 'WISCONSIN', 'ISRAEL', 'NEW MEXICO',
         'UNITED ARAB EMIRATES', 'AUSTRALIA', 'DIST. OF COLUMBIA',
         'SOUTH AFRICA', 'UNITED KINGDOM', 'WASHINGTON', 'MAINE', 'GREECE',
         'MOROCCO', 'FRANCE', 'HUNGARY', 'ARKANSAS', 'NEW HAMPSHIRE',
         'COLOMBIA', 'RUSSIA', 'MEXICO', 'VERMONT', 'JAPAN', 'IRELAND',
         'NEVADA', 'LOUISIANA', 'IDAHO', 'UTAH', 'BRAZIL', 'GUATEMALA',
         'DENMARK', 'VIET-NAM', 'CANADA', 'GERMANY', 'NETHERLANDS',
         'OKLAHOMA', 'SWEDEN'
        ],
        "Housing": [
          'Off-Campus', 'ULH', 'ULP', 'AFF', 'NIN', 'SR', 'N', 'CLB', 'ULN'
        ],
        "Degree": [
          'Undeclared', 'BSB', 'BSE', 'BA', 'BSW', 'BS', 'BM', 'BBA', 'BSN'
        ],
        "Address Type": [
          'Off-Campus', 'DORM', 'AFLT'
        ],
        "First Time Student": [
          'Y', 'N', 'S'
        ],
        "HSG Source": [
          'None', 'ULH', 'ULP', 'ARC', 'NIN', 'CLB', 'PRV', 'SR'
        ],
        "STEM Degree": [
          'Y', 'N'
        ],
        "GRS": [
          'Y', 'N', 'P'
        ],
      },
      studentInfo: {
        'Permanent ZIP': '',
        'GPA': 0,
        "ACT Comp": 0,
      }
    }
  },
  methods: {
    predict() {

    }
  },
  mounted() {
    for (const propertyName in this.dataValues) {
      this.studentInfo[propertyName] = ''
    }
  }
}
</script>

<style scoped>
select {
  color: inherit !important;
}

form label {
  @apply text-[1.1rem] capitalize mb-2 block;
  font-family: 'Montserrat Alternates', sans-serif;
}

#student-info form select {
  @apply text-gray-600 mb-2 block;
  font-family: 'Montserrat Alternates', sans-serif;
}

form select {
  @apply bg-white py-3 px-3 rounded-xl text-[.9rem] max-w-full w-full outline-none;
  color: white;
}

form input {
  @apply bg-white py-2 px-3 rounded-xl text-[.9rem] max-w-full outline-none w-full;
}

input[type='radio'] {
  @apply absolute;
  clip: rect(0, 0, 0, 0);
}

input[type='radio'] + label::before {
  @apply w-4 h-4 bg-white rounded-full inline-block mr-3 mt-1 transition-all ease-in-out duration-300;
  content: '';
  box-shadow: 0 0 0 0.25rem #0c224b58;
}

svg {
  @apply fill-current;
}

input[type='radio'] + label {
  @apply cursor-pointer;
  font-family: syne !important;
}

input[type='radio']:checked + label::before {
  @apply bg-blue;
}

.theme-red {
  @apply py-10;
}

.theme-red select,
.theme-red input {
  @apply bg-[#FFEDED] !important;
}

.theme-red input[type='radio'] + label::before {
  box-shadow: 0 0 0 0.25rem #F4DBDB;
}
</style>
