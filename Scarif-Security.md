# Scarif Security

## Daxili Təhlükəsizlik İnfrastrukturunun Qurulması və Analizi

**Windows Server əsaslı korporativ şəbəkə infrastrukturunun tətbiqi**

- **Hazırlayan:** Melisa Hacızadə
- **Təşkilat:** Scarif Security
- **Layihə mühiti:** Windows Server əsaslı korporativ laboratoriya infrastrukturu
- **Domen:** `scarif.local`
- **Tarix:** Mart 2026

## İstifadə olunan əsas texnologiyalar
- Microsoft Windows Server
- Active Directory Domain Services (AD DS)
- Organizational Unit (OU) strukturu
- Group Policy Management (GPO)
- File Server və Access Control
- Internet Information Services (IIS)
- Domain əsaslı istifadəçi autentifikasiyası
# **MÜNDƏRİCAT**

## **Giriş**
# 1. Active Directory Domen İnfrastrukturunun Qurulması

1.1 Bölmənin məqsədi
1.2 Şəbəkə və sistemin ilkin konfiqurasiyası
1.3 Active Directory Domain Services rolunun quraşdırılması
1.4 Domenin yaradılması
1.4.1 Domen məlumatlarının yoxlanılması
1.4.2 Forest strukturunun yoxlanılması
1.4.3 Domain Controller rolunun təsdiqi
1.4.4 SYSVOL və NETLOGON paylaşımlarının yoxlanılması
1.4.5 Ümumi sağlamlıq testi

# 2. Organizational Unit (OU) Strukturu

2.1 Mövcud OU strukturu

2.2 OU-ların PowerShell vasitəsilə yoxlanılması

2.3 Strukturun praktiki istifadəsi

# 3. İstifadəçilərin CSV vasitəsilə avtomatik yaradılması

3.1 İstifadə olunan məlumat mənbəyi
3.2 PowerShell skriptinin işləmə prinsipi
3.3 İstifadə olunan skript
3.4 Yaradılma nəticəsi
3.5 Yaradılan istifadəçilərin yoxlanılması
3.6 Parol siyasətinin yoxlanılması

# 4. Security Group strukturu və RBAC modeli

4.1 Department əsaslı Security Group-ların yaradılması
4.2 İstifadəçilərin avtomatik olaraq qruplara əlavə edilməsi
4.3 Qrup üzvlüyünün yoxlanılması
4.4 RBAC modelinin məntiqi quruluşu
4.5 İstifadəçi səviyyəsində qrup üzvlüyünün yoxlanılması
4.6 Nəticə

# 5. File Server Strukturunun Yoxlanılması və İcazə Modeli

5.1 Qovluq strukturunun yoxlanılması
5.2 SMB Share-lərin yoxlanılması
5.3 Share səviyyəsində icazələrin yoxlanılması
5.4 NTFS icazələrinin yoxlanılması
5.5 İstifadəçi qrup üzvlüyünün yoxlanılması

# 6. File Server Access Testləri

6.1 IT qovluğuna giriş
6.2 Digər departament qovluğuna giriş
6.3 Nəticə

# 7. Group Policy Object (GPO) Konfiqurasiyası

7.1 Domen daxilində mövcud GPO-ların siyahısı
7.2 HR departamenti üçün tətbiq olunan siyasətlər
7.3 Finance departamenti üçün tətbiq olunan siyasətlər
7.4 IT departamenti üçün tətbiq olunan siyasətlər
7.5 Digər departamentlər üçün standart GPO
7.6 Default Domain Policy üzərində edilmiş dəyişikliklər
7.7 Domain Wallpaper GPO
7.8 GPO strukturunun dizayn prinsipi
7.9 GPO siyasətlərinin client sistem üzərində test edilməsi

# 8. IIS Server və Web Portalın Qurulması

8.1 IIS Web Server rolunun quraşdırılması
8.2 IIS saytlarının konfiqurasiyası
8.3 Portalın fiziki fayl strukturu
8.4 HTTPS binding konfiqurasiyası
8.5 SSL sertifikatının tətbiqi
8.6 Authentication konfiqurasiyası
8.7 IIS xidmətinin statusu
8.8 Portalın test edilməsi və təhlükəsizlik analizi

# 9. Nəticə

> **Note:** This repository contains documentation of a Windows Server-based laboratory environment. Credentials shown in the original report have been redacted before publication.

# Giriş

Müasir təşkilatlarda informasiya sistemlərinin təhlükəsiz və effektiv şəkildə idarə olunması üçün mərkəzləşdirilmiş şəbəkə infrastrukturu böyük əhəmiyyət daşıyır. Korporativ şəbəkə mühitlərində istifadəçilərin, kompüterlərin və sistem resurslarının idarə olunması üçün Microsoft Windows Server platforması geniş istifadə olunur. Bu platforma Active Directory, Group Policy və digər idarəetmə mexanizmləri vasitəsilə təşkilat daxilində təhlükəsizlik və idarəetmə proseslərinin mərkəzləşdirilmiş şəkildə həyata keçirilməsinə imkan verir.

Bu layihə çərçivəsində Windows Server əsaslı korporativ şəbəkə mühitinin qurulması və əsas təhlükəsizlik mexanizmlərinin tətbiqi həyata keçirilmişdir. Layihənin əsas məqsədi müəssisə səviyyəsində istifadə olunan şəbəkə idarəetmə və təhlükəsizlik prinsiplərini praktik laboratoriya mühitində tətbiq etmək və onların işləmə mexanizmini analiz etməkdir.

Layihə daxilində Microsoft Active Directory Domain Services (AD DS) infrastrukturu qurulmuş və scarif.local domen mühiti yaradılmışdır. Domen infrastrukturu istifadəçilərin və kompüterlərin mərkəzləşdirilmiş şəkildə idarə olunmasını təmin edir. Bundan əlavə, təşkilat daxilində müxtəlif şöbələri əhatə edən Organizational Unit (OU) strukturu yaradılmış və istifadəçilər müvafiq departamentlər üzrə təşkil edilmişdir. Bu yanaşma idarəetməni sadələşdirir və təhlükəsizlik siyasətlərinin departamentlər üzrə tətbiq olunmasına imkan verir.

İstifadəçi və sistem idarəetməsini daha effektiv həyata keçirmək məqsədilə Group Policy mexanizmlərindən istifadə edilmişdir. Bu siyasətlər vasitəsilə sistem konfiqurasiyaları, təhlükəsizlik parametrləri və istifadəçi mühitinin idarə olunması mərkəzləşdirilmiş şəkildə həyata keçirilir.

Layihə çərçivəsində həmçinin təşkilat daxilində istifadə olunan resursların idarə olunması üçün File Server infrastrukturu qurulmuş və departament əsaslı paylaşım qovluqları yaradılmışdır. NTFS icazələri və təhlükəsizlik qrupları vasitəsilə istifadəçilərin resurslara giriş hüquqları idarə olunmuşdur.

Bundan əlavə, Microsoft Internet Information Services (IIS) platforması üzərində daxili veb portal hazırlanmışdır. Bu portal təşkilat daxilində istifadə olunan əməkdaş kataloqu (Employee Directory) kimi fəaliyyət göstərir və istifadəçilərin domen autentifikasiyası vasitəsilə sistemə girişini təmin edir. Beləliklə, yalnız domen istifadəçilərinin daxili veb servisə girişinə icazə verilir.

Hazırlanmış laboratoriya infrastrukturu real korporativ şəbəkə mühitlərində istifadə olunan idarəetmə və təhlükəsizlik prinsiplərinə uyğun şəkildə dizayn edilmişdir. Bu hesabat layihə çərçivəsində qurulmuş sistem arxitekturasını, tətbiq olunan texnologiyaları və həyata keçirilmiş konfiqurasiya mərhələlərini ətraflı şəkildə təqdim edir.

## Active Directory Domen İnfrastrukturunun Qurulması

## 1.1 Bölmənin məqsədi

Bu bölmədə təşkilat daxilində mərkəzləşdirilmiş identifikasiya və idarəetmə mexanizminin yaradılması məqsədilə Microsoft Active Directory əsaslı domen mühitinin qurulması və ilkin konfiqurasiyası təqdim olunur.

Active Directory domen infrastrukturu aşağıdakı funksiyaları təmin edir:

İstifadəçi və kompüterlərin mərkəzləşdirilmiş idarə olunması

Autentifikasiya və avtorizasiya mexanizmi

Group Policy vasitəsilə konfiqurasiya nəzarəti

Təhlükəsizlik siyasətlərinin tətbiqi üçün struktur baza

Bu mərhələdə domen yaradılmış, DNS inteqrasiyası həyata keçirilmiş və sistemin funksionallığı yoxlanılmışdır.

## 1.2 Şəbəkə və sistemin ilkin konfiqurasiyası

Domen Controller server statik IP ünvanı ilə konfiqurasiya edilmişdir. Statik IP istifadəsi domen mühitində sabitliyin qorunması üçün vacibdir.

Server parametrləri:

IP ünvanı: 192.168.20.10

Subnet maska: 255.255.255.0

Default gateway: 192.168.20.253

DNS server: 192.168.20.10

IP konfiqurasiyasının yoxlanılması:

Get-NetIPAddress -AddressFamily IPv4

## 1.3 Active Directory Domain Services rolunun quraşdırılması

Active Directory Domain Services (AD DS) rolu aşağıdakı əmrlə quraşdırılmışdır:

Install-WindowsFeature AD-Domain-Services -IncludeManagementTools

Bu əmrin icrası nəticəsində:

Active Directory servisləri sistemə əlavə edilmişdir

İdarəetmə alətləri (ADUC, GPMC və s.) aktivləşdirilmişdir

DNS idarəetmə modulları quraşdırılmışdır

## 1.4 Domenin yaradılması

Layihə mühitində Active Directory Domain Services (AD DS) artıq qurulmuş vəziyyətdə olmuşdur. Bu bölmədə domen strukturunun düzgün və funksional vəziyyətdə olduğunu təsdiq etmək məqsədilə sistem səviyyəsində texniki yoxlamalar aparılmışdır.

## 1.4.1 Domen Məlumatlarının Yoxlanılması

Active Directory domen obyektinin mövcudluğu və struktur parametrləri aşağıdakı əmr vasitəsilə analiz edilmişdir:

Get-ADDomain

Yoxlama nəticəsində:

Domen adı: scarif.local

NetBIOS adı: SCARIF

Domain Mode: Windows Server səviyyəsi

PDC Emulator və RID Master rolları aktiv

Bu nəticə domen obyektinin sistemdə düzgün formalaşdığını göstərir.

## 1.4.2 Forest Strukturunun Yoxlanılması

Forest səviyyəsinin və root domenin vəziyyəti aşağıdakı əmr ilə təsdiq edilmişdir:

Get-ADForest

Nəticə:

Root Domain: scarif.local

Forest Mode: Uyğun Windows Server səviyyəsi

Domains siyahısında scarif.local mövcuddur

Bu, forest arxitekturasının aktiv və sağlam olduğunu göstərir.

## 1.4.3 Domain Controller Rolunun Təsdiqi

Serverin Domain Controller kimi fəaliyyət göstərdiyini yoxlamaq üçün:

Get-ADDomainController

Nəticə:

HostName: ADDC.scarif.local

IPv4: 192.168.20.10

IsGlobalCatalog: True

Bu göstəricilər serverin əsas DC kimi işlədiyini təsdiq edir.

## 1.4.4 SYSVOL və NETLOGON Paylaşımlarının Yoxlanılması

GPO və autentifikasiya mexanizmlərinin işləkliyini təsdiq etmək məqsədilə aşağıdakı əmr icra edilmişdir:

net share

SYSVOL və NETLOGON paylaşımlarının mövcudluğu domen xidmətlərinin düzgün konfiqurasiya edildiyini göstərir.

## 1.4.5 Ümumi Sağlamlıq Testi

Active Directory xidmətlərinin ümumi sağlamlıq vəziyyəti aşağıdakı diaqnostik alət vasitəsilə yoxlanılmışdır:

dcdiag

Nəticə: Kritik xəta aşkarlanmamışdır.

Organizational Unit Strukturu

Domen daxilində department əsaslı OU strukturu mövcuddur. Bütün department-lər “Scarif Security” adlı əsas OU altında yerləşdirilmişdir.

## 2.1 Mövcud Struktur

scarif.local
 └── Scarif Security
      ├── Customer Support
      ├── Engineering
      ├── Executive
      ├── Facilities
      ├── Finance
      ├── HR
      ├── IT
      ├── Legal
      ├── Marketing
      ├── Operations
      ├── Sales
      ├── Security
      └── Workstations

Bu struktur:

İstifadəçilərin department üzrə ayrılması

GPO-ların department üzrə tətbiqi

Security Group-ların düzgün işləməsi

üçün istifadə olunur.

## 2.2 OU-ların Yoxlanılması

Get-ADOrganizationalUnit -Filter * | Select Name, DistinguishedName

Nəticədə bütün department OU-ları siyahıda görünür.

## 2.3 Strukturun Praktiki İstifadəsi

Hər department istifadəçiləri öz OU-sunda yerləşdirilib

GPO-lar OU-lara link edilib

File access Security Group-lar vasitəsilə idarə olunur

Workstations OU-sunda domain-ə qoşulmuş client kompüterlər yerləşdirilir

Bu model real korporativ mühitdə istifadə olunan department-based AD dizaynına uyğundur.

# 3. İstifadəçilərin CSV vasitəsilə avtomatik yaradılması

Domen mühitində 100 istifadəçinin manual şəkildə yaradılması əvəzinə proses PowerShell skripti vasitəsilə avtomatlaşdırılmışdır. İstifadəçi məlumatları strukturlaşdırılmış CSV fayldan oxunaraq müvafiq OU-lara yerləşdirilmişdir.

## 3.1 İstifadə olunan məlumat mənbəyi

İstifadəçi məlumatları aşağıdakı sahələri əhatə edən users.csv faylından götürülmüşdür:

FirstName

LastName

FatherName

SamAccountName

Department

Title

Office

Mobile

EmployeeID

StartDate

## 3.2 PowerShell skriptinin işləmə prinsipi

Skript aşağıdakı mərhələlərlə işləyir:

Active Directory modulunun yüklənməsi

CSV faylın import edilməsi

Department əsasında düzgün OU yolunun formalaşdırılması

Duplicate SamAccountName yoxlanışı

İstifadəçinin yaradılması

Hesabın aktivləşdirilməsi və ilk girişdə parol dəyişmə məcburiyyəti

## 3.3 İstifadə olunan skript

Import-Module ActiveDirectory

$CSVPath = "C:\scripts\users.csv"
$Users = Import-Csv $CSVPath

$Domain = "scarif.local"
$BaseOU = "OU=Scarif Security,DC=scarif,DC=local"

$DefaultPassword = ConvertTo-SecureString "<REDACTED>" -AsPlainText -Force

foreach ($User in $Users) {

    $Department = $User.Department.Trim()
    $Sam = $User.SamAccountName.Trim()
    $UPN = "$Sam@$Domain"
    $OUPath = "OU=$Department,$BaseOU"

    $ExistingUser = Get-ADUser -Filter "SamAccountName -eq '$Sam'" -ErrorAction SilentlyContinue

    if (-not $ExistingUser) {

        New-ADUser `
        -Name "$($User.FirstName) $($User.LastName) - $($User.EmployeeID)" `
        -GivenName $User.FirstName `
        -Surname $User.LastName `
        -OtherName $User.FatherName `
        -DisplayName "$($User.FirstName) $($User.LastName)" `
        -SamAccountName $Sam `
        -UserPrincipalName $UPN `
        -EmailAddress $UPN `
        -Department $Department `
        -Title $User.Title `
        -Office $User.Office `
        -MobilePhone $User.Mobile `
        -EmployeeID $User.EmployeeID `
        -Description "StartDate: $($User.StartDate)" `
        -Path $OUPath `
        -AccountPassword $DefaultPassword `
        -Enabled $true `
        -ChangePasswordAtLogon $true

        Write-Host "$Sam created successfully"
    }
    else {
        Write-Host "$Sam already exists"
    }
}

## 3.4 Yaradılma nəticəsi

PowerShell çıxışında istifadəçilərin uğurla yaradıldığı görünür:

Bu çıxış hər bir istifadəçinin AD-də uğurla yaradıldığını göstərir.

## 3.5 Yaradılan istifadəçilərin yoxlanılması

İstifadəçilərin CSV-dən düzgün yaradıldığını və müvafiq department atributunun doldurulduğunu təsdiqləmək üçün bütün domen üzrə “Department” field-i əsasında qruplaşdırma aparılmışdır.

Əmr (Department üzrə sayların yoxlanması):

Get-ADUser -Filter * -Properties Department |
Group-Object Department |
Select Name,Count

### Nəticə (çıxışın interpretasiyası):

Department-lər üzrə istifadəçi sayı ayrı-ayrılıqda görünür (məsələn: Engineering, Sales, Finance, IT və s.).

Bu nəticə CSV import prosesində Department atributunun düzgün yazıldığını və istifadəçilərin kütləvi yaradıldığını göstərir.

Department məlumatı olmayan hesabların aşkar edilməsi

CSV ilə yaradılan biznes user-lar üçün Department sahəsinin boş qalması normativ deyil. Ona görə ayrıca audit aparılıb və Department field-i boş olan account-lar çıxarılmışdır.

Əmr (Department boş olan user-ların tapılması):

Get-ADUser -Filter * -Properties Department |
Where-Object { -not $_.Department } |
Select Name,SamAccountName

Nəticə:

Çıxışda yalnız standart sistem hesabları görünür:

administrator

guest

krbtgt

svc_iis

Bu normaldır və gözləniləndir:

Administrator və Guest built-in hesabdır.

krbtgt Kerberos üçün sistem hesabıdır. svc_iis IIS Server üçün yaradılmış hesabdır.
Bu hesabların Department dəyərinin boş olması konfiqurasiya xətası sayılmır.

Seçilmiş istifadəçinin tam atribut audit yoxlanılması

Kütləvi yaradılma prosesinin düzgün icra olunduğunu sübut etmək üçün seçilmiş bir istifadəçinin bütün atributları detallı şəkildə yoxlanılmışdır.

Get-ADUser aveliyev -Properties GivenName,
Surname,
OtherName,
SamAccountName,
UserPrincipalName,
EmailAddress,
Department,
Title,
Office,
MobilePhone,
EmployeeID,
Description,
Enabled,
DistinguishedName |
Select GivenName,
Surname,
OtherName,
SamAccountName,
UserPrincipalName,
EmailAddress,
Department,
Title,
Office,
MobilePhone,
EmployeeID,
Description,
Enabled,
DistinguishedName

Yoxlanılan sahələr

Ad və Soyad (GivenName, Surname)

Ata adı (OtherName)

SamAccountName

UserPrincipalName

EmailAddress

Department

Title

Office

MobilePhone

EmployeeID

Description (StartDate məlumatı)

Enabled statusu

DistinguishedName (OU yerləşməsi)

Analiz

Nəticə göstərir ki:

İstifadəçinin adı və soyadı CSV ilə uyğun gəlir

Ata adı düzgün yazılıb

E-mail və UPN domen formatında yaradılıb

Department düzgün təyin olunub

Telefon nömrəsi və Office məlumatı əlavə edilib

EmployeeID unikal olaraq yazılıb

Hesab aktivdir (Enabled = True)

İstifadəçi düzgün OU daxilində yerləşdirilib

Description sahəsində StartDate saxlanılıb

Məsələn:

CN=User Name - 1023
OU=IT
OU=Scarif Security
DC=scarif
DC=local

Bu isə istifadəçinin düzgün department OU-sunda yaradıldığını təsdiqləyir.

Parol siyasətinin yoxlanılması

İstifadəçinin ilk girişdə parol dəyişmə tələbinin icra vəziyyəti aşağıdakı əmrlə yoxlanılmışdır:

Get-ADUser aveliyev -Properties PasswordLastSet |
Select SamAccountName,PasswordLastSet

Analiz

PasswordLastSet sahəsinin dəyəri mövcuddur.

Bu, istifadəçinin parolu artıq dəyişdiyini göstərir.

Hesab aktiv şəkildə istifadə olunmuşdur.

İlkin təhlükəsizlik siyasəti tətbiq edilmiş və icra olunmuşdur.

Əgər PasswordLastSet boş və ya 0 olsaydı, bu istifadəçinin hələ sistemə daxil olmadığını göstərərdi.

4.Security Group strukturu və RBAC modeli

İstifadəçi hesabları yaradıldıqdan sonra növbəti mərhələdə departament əsaslı təhlükəsizlik modeli formalaşdırılmışdır. Bu mərhələdə istifadəçilərə birbaşa icazə verilməmiş, səlahiyyətlər təhlükəsizlik qrupları vasitəsilə idarə edilmişdir.

Hər departament üçün ayrıca Global tipli Security Group yaradılmışdır. Qrup adlandırma standartı aşağıdakı formada tətbiq edilmişdir:

SG_DepartmentName_Modify

Bu adlandırma həm oxunaqlılığı, həm də gələcək genişlənmə imkanını təmin edir.

## 4.1 Department əsaslı Security Group-ların yaradılması

Active Directory-də mövcud departament OU-ları dinamik şəkildə oxunmuş və hər biri üçün uyğun təhlükəsizlik qrupu yaradılmışdır.

İcra olunmuş əmrlər:

Nəticədə aşağıdakı qruplar yaradılmışdır:

SG_IT_Modify

SG_HR_Modify

SG_Finance_Modify

SG_Engineering_Modify

SG_Sales_Modify

və digər departamentlər üzrə analoji qruplar

Bütün qruplar Global Scope və Security tipində konfiqurasiya edilmişdir.

## 4.2 İstifadəçilərin avtomatik olaraq qruplara əlavə edilməsi

CSV-dən yaradılmış istifadəçilər avtomatik olaraq öz departamentlərinə uyğun qruplara əlavə edilmişdir.

foreach ($User in $Users) {

    $Dept = $User.Department.Replace(" ","")
    $GroupName = "SG_${Dept}_Modify"

    Add-ADGroupMember -Identity $GroupName -Members $User.SamAccountName
}

Bu mərhələdən sonra:

Hər istifadəçi yalnız öz departament qrupunun üzvüdür

Birbaşa user-based permission tətbiq edilməmişdir

İdarəetmə qrup səviyyəsində aparılır

Bu model gələcəkdə istifadəçi dəyişikliklərini sadələşdirir.

## 4.3 Qrup üzvlüyünün yoxlanılması

IT qrupu üzrə yoxlama

Get-ADGroupMember SG_IT_Modify |
Select Name,SamAccountName

Bu çıxış IT department istifadəçilərinin düzgün şəkildə qrupa əlavə edildiyini göstərir.

## 4.4 RBAC Modelinin Məntiqi Quruluşu

Qurulmuş təhlükəsizlik modeli Role-Based Access Control (RBAC) prinsipi əsasında təşkil edilmişdir. Səlahiyyət axını aşağıdakı ardıcıllıqla formalaşdırılmışdır:

User → Department OU
User → Security Group
Security Group → File Server icazəsi

Bu modeldə istifadəçi ilə resurs arasında birbaşa əlaqə mövcud deyil. İcazələr yalnız təhlükəsizlik qrupları vasitəsilə tətbiq olunur.

Qurulmuş mexanizmin əsas xüsusiyyətləri:

İstifadəçilərə birbaşa NTFS və ya Share icazəsi verilməmişdir

İstifadəçinin departamenti dəyişdirildikdə və ya qrup üzvlüyü yeniləndikdə icazələr avtomatik şəkildə yenilənir

Səlahiyyət idarəetməsi mərkəzləşdirilmiş və standartlaşdırılmış şəkildə aparılır

Struktur daha təhlükəsiz, genişlənə bilən və idarəolunandır

Bu yanaşma korporativ Active Directory mühitlərində tətbiq edilən standart təhlükəsizlik praktikasına uyğundur.

## 4.5 İstifadəçi Səviyyəsində Qrup Üzvlüyünün Yoxlanılması

RBAC modelinin düzgün tətbiq olunduğunu təsdiqləmək məqsədilə seçilmiş istifadəçi üzrə qrup üzvlüyü yoxlanılmışdır.

### İcra olunan əmr:

Get-ADUser aveliyev -Properties MemberOf |
Select -ExpandProperty MemberOf

Yoxlama nəticəsində istifadəçinin yalnız öz departamentinə uyğun təhlükəsizlik qrupunun üzvü olduğu müəyyən edilmişdir. Bu, səlahiyyətlərin departament əsaslı və məhdudlaşdırılmış şəkildə tətbiq edildiyini göstərir.

Bu mərhələ RBAC modelinin praktik təsdiqi kimi qiymətləndirilə bilər.

## 4.6 Nəticə

4-cü bölmə üzrə aparılmış konfiqurasiya nəticəsində aşağıdakı struktur formalaşdırılmışdır:

Department əsaslı Security Group modeli qurulmuşdur

İstifadəçilər avtomatlaşdırılmış skript vasitəsilə müvafiq qruplara əlavə edilmişdir

RBAC prinsipi real mühitdə tətbiq olunmuşdur

İcazə idarəetməsi istifadəçi səviyyəsində deyil, qrup səviyyəsində həyata keçirilir

File Server Strukturunun Yoxlanılması və İcazə Modeli

Bu mərhələdə server üzərində yaradılmış departament qovluqları, şəbəkə paylaşımları və tətbiq edilmiş icazələr PowerShell vasitəsilə yoxlanılmışdır. Məqsəd departament əsaslı qovluq strukturunun və təhlükəsizlik qrupları vasitəsilə tətbiq edilmiş RBAC modelinin düzgün işlədiyini təsdiqləmək olmuşdur.

## 5.1 Qovluq Strukturunun Yoxlanılması

Server üzərində departament məlumatlarının saxlanıldığı əsas qovluğun mövcudluğu yoxlanılmışdır.

### İcra olunan əmr:

Test-Path "C:\CompanyData\Departments"

Nəticədə qovluğun server üzərində mövcud olduğu təsdiqlənmişdir.

(Şəkil 5.1 – Departments qovluğunun mövcudluğunun yoxlanılması)

Daha sonra həmin qovluq daxilində yerləşən departament qovluqları siyahıya alınmışdır.

### İcra olunan əmr:

Get-ChildItem "C:\CompanyData\Departments" | Select Name

### Əmr nəticəsində server üzərində yaradılmış departament qovluqları siyahıya alınmışdır.

(Şəkil 5.2 – Departament qovluqlarının siyahısı)

Bu nəticə server üzərində bütün departamentlər üçün ayrıca qovluq strukturunun yaradıldığını və strukturun Active Directory-də təşkil edilmiş departament modelinə uyğun olduğunu göstərir.

## 5.2 SMB Share-lərin Yoxlanılması

Departament qovluqlarının şəbəkə üzərindən paylaşılması aşağıdakı PowerShell əmri vasitəsilə yoxlanılmışdır.

### İcra olunan əmr:

Get-SmbShare | Select Name,Path

### Əmr nəticəsində departament qovluqlarının server üzərində şəbəkə paylaşımı kimi aktiv olduğu müəyyən edilmişdir.

(Şəkil 5.3 – Server üzərində aktiv SMB paylaşımları)

Bundan əlavə Windows Server tərəfindən avtomatik yaradılan aşağıdakı sistem paylaşımları da müşahidə edilmişdir:

ADMIN$

C$

IPC$

NETLOGON

SYSVOL

Bu paylaşımlar Active Directory və Windows xidmətlərinin işləməsi üçün tələb olunur.

## 5.3 Share Səviyyəsində İcazələrin Yoxlanılması

IT departament qovluğu üçün tətbiq edilmiş share səviyyəli icazələr aşağıdakı əmr vasitəsilə yoxlanılmışdır.

### İcra olunan əmr:

Get-SmbShareAccess -Name "IT"

Nəticədə IT departament qovluğuna giriş icazəsinin SCARIF\SG_IT_Modify təhlükəsizlik qrupuna verildiyi müəyyən edilmişdir.

(Şəkil 5.4 – IT departamenti üçün share icazələrinin yoxlanılması)

Bu nəticə göstərir ki, icazələr istifadəçilərə birbaşa verilməmiş, təhlükəsizlik qrupları vasitəsilə idarə olunmuşdur.

## 5.4 NTFS İcazələrinin Yoxlanılması

Qovluq səviyyəsində tətbiq olunmuş NTFS icazələri aşağıdakı əmr vasitəsilə yoxlanılmışdır.

### İcra olunan əmr:

(Get-Acl "C:\CompanyData\Departments\IT").Access |

Where-Object { $_.IdentityReference -like "*IT*" }

Nəticədə IT qovluğu üçün aşağıdakı icazənin tətbiq edildiyi müəyyən edilmişdir:

SCARIF\SG_IT_Modify → Modify

(Şəkil 5.5 – IT qovluğu üçün NTFS icazələrinin yoxlanılması)

Bu nəticə göstərir ki, qovluq üzərində icazə yalnız müvafiq təhlükəsizlik qrupuna verilmişdir və istifadəçilərə birbaşa icazə təyin edilməmişdir.

## 5.5 İstifadəçi Qrup Üzvlüyünün Yoxlanılması

RBAC modelinin düzgün işlədiyini təsdiqləmək üçün seçilmiş istifadəçinin təhlükəsizlik qruplarına üzvlüyü Active Directory səviyyəsində yoxlanılmışdır.

Test istifadəçi: aveliyev

İstifadəçinin daxil olduğu təhlükəsizlik qruplarını müəyyən etmək üçün aşağıdakı PowerShell əmri icra edilmişdir.

Get-ADPrincipalGroupMembership aveliyev | Select Name

### Əmr nəticəsində istifadəçinin aşağıdakı qruplara üzv olduğu müəyyən edilmişdir:

Domain Users

SG_IT_Modify

(Şəkil 5.6 – İstifadəçinin təhlükəsizlik qrup üzvlüyü)

Bu nəticə göstərir ki, istifadəçi IT departamenti üçün yaradılmış SG_IT_Modify təhlükəsizlik qrupunun üzvüdür və bu qrup vasitəsilə departament qovluğuna giriş icazəsinə malikdir.

Beləliklə, icazələrin istifadəçi səviyyəsində deyil, Security Group vasitəsilə idarə olunduğu RBAC modeli düzgün şəkildə tətbiq edilmişdir.

File Server Access Testləri

Bu mərhələdə departament əsaslı icazə modelinin düzgün işlədiyini yoxlamaq üçün real istifadəçi hesabı ilə File Server üzərində giriş testləri aparılmışdır.

Server ünvanı:

\\192.168.20.10

## 6.1 IT Qovluğuna Giriş

IT departament istifadəçisi aveliyev hesabı ilə aşağıdakı qovluğa giriş yoxlanılmışdır.

\\192.168.20.10\IT

Nəticə:

İstifadəçi qovluğa uğurla daxil olmuşdur.

(Şəkil 6.1 – IT qovluğuna uğurlu giriş)

## 6.2 Digər Departament Qovluğuna Giriş

Eyni istifadəçi hesabı ilə digər departament qovluqlarına giriş yoxlanılmışdır.

\\192.168.20.10\HR

Nəticə:

İstifadəçinin bu qovluğa girişinə icazə verilməmişdir.

(Şəkil 6.2 – HR qovluğuna girişin məhdudlaşdırılması)

## 6.3 Nəticə

Test nəticəsində istifadəçinin yalnız öz departamentinə aid qovluğa giriş əldə etdiyi, digər departament qovluqlarına girişin isə məhdudlaşdırıldığı təsdiqlənmişdir. Bu, File Server üzərində RBAC modelinin düzgün tətbiq edildiyini göstərir.

# 7. Group Policy Object (GPO) konfiqurasiyası

Active Directory mühitində istifadəçi və kompüter konfiqurasiyalarını 2mərkəzləşdirilmiş şəkildə idarə etmək üçün Group Policy Object (GPO) mexanizmindən istifadə edilmişdir.

Group Policy vasitəsilə istifadəçilərin sistem üzərində səlahiyyətləri məhdudlaşdırılmış, təhlükəsizlik siyasətləri tətbiq edilmiş və departamentlər üzrə fərqli idarəetmə modeli qurulmuşdur.

Layihə çərçivəsində GPO-lar aşağıdakı iki səviyyədə tətbiq edilmişdir:

User Configuration – istifadəçilərin sistemdə edə biləcəyi əməliyyatları idarə edir

Computer Configuration – kompüter səviyyəsində təhlükəsizlik və şəbəkə parametrlərini idarə edir

## 7.1 Domen daxilində mövcud GPO-ların siyahısı

Domen mühitində yaradılmış bütün Group Policy obyektlərini əldə etmək üçün aşağıdakı PowerShell əmri istifadə edilmişdir.

### İcra olunan əmr

Get-GPO -All | Select DisplayName

### Əmr nəticəsində domen daxilində yaradılmış bütün Group Policy obyektləri siyahıya alınmışdır.

(Şəkil 7.1 – Domen daxilində mövcud GPO-ların siyahısı)

## 7.2 HR departamenti üçün tətbiq olunan siyasətlər

HR departamenti üçün istifadəçi səviyyəsində məhdudlaşdırıcı siyasətlər tətbiq edilmişdir. Bu siyasətlər istifadəçilərin sistem konfiqurasiyasını dəyişməsinin qarşısını almaq məqsədilə tətbiq edilmişdir.

User səviyyəsində tətbiq olunan siyasətlər

HR istifadəçiləri üçün aşağıdakı məhdudiyyətlər tətbiq edilmişdir:

Start Menu üzərindən Run menyusu deaktiv edilmişdir

Command Prompt istifadəsi bloklanmışdır

PowerShell istifadəsi bloklanmışdır

Control Panel girişinə məhdudiyyət tətbiq edilmişdir

Bu siyasətlər istifadəçilərin sistem üzərində inzibati dəyişikliklər etməsinin qarşısını almaq məqsədilə tətbiq edilmişdir.

Computer səviyyəsində tətbiq olunan siyasətlər

HR kompüterləri üçün aşağıdakı təhlükəsizlik parametrləri tətbiq edilmişdir:

Windows Defender Firewall aktiv edilmişdir

Removable storage cihazları üçün write access deaktiv edilmişdir

Multicast name resolution deaktiv edilmişdir

Bu konfiqurasiyalar sistem təhlükəsizliyinin artırılması və məlumat sızmasının qarşısının alınması məqsədilə tətbiq edilmişdir.

## 7.3 Finance departamenti üçün tətbiq olunan siyasətlər

Finance departamenti maliyyə məlumatları ilə işlədiyi üçün bu departament üçün daha sərt təhlükəsizlik siyasətləri tətbiq edilmişdir.

User səviyyəsində tətbiq olunan siyasətlər

Finance istifadəçiləri üçün aşağıdakı məhdudiyyətlər tətbiq edilmişdir:

Control Panel istifadəsi bloklanmışdır

Command Prompt istifadəsi bloklanmışdır

PowerShell istifadəsi bloklanmışdır

C disk bölməsinə giriş məhdudlaşdırılmışdır

Bu siyasətlər maliyyə məlumatlarının qorunmasını təmin etmək məqsədilə tətbiq edilmişdir.

Computer səviyyəsində tətbiq olunan siyasətlər

Finance kompüterləri üçün aşağıdakı təhlükəsizlik konfiqurasiyaları tətbiq edilmişdir:

Windows Defender Firewall aktiv edilmişdir

Removable disk-lər üçün write access deaktiv edilmişdir

Multicast name resolution deaktiv edilmişdir

Bu siyasətlər maliyyə məlumatlarının qorunması və sistem təhlükəsizliyinin təmin edilməsi məqsədilə tətbiq edilmişdir.

## 7.4 IT departamenti üçün tətbiq olunan siyasətlər

IT departamenti sistem administrasiyası və texniki xidmət funksiyalarını yerinə yetirdiyi üçün digər departamentlərlə müqayisədə daha az məhdudiyyət tətbiq edilmişdir.

User səviyyəsində tətbiq olunan siyasətlər

IT istifadəçiləri üçün yalnız aşağıdakı məhdudiyyət tətbiq edilmişdir:

Control Panel girişinə məhdudiyyət

Command Prompt və digər idarəetmə vasitələri IT istifadəçiləri üçün açıq saxlanılmışdır.

Computer səviyyəsində tətbiq olunan siyasətlər

IT kompüterləri üçün aşağıdakı təhlükəsizlik konfiqurasiyaları tətbiq edilmişdir:

Windows Defender Firewall aktiv edilmişdir

Inbound bağlantılar bloklanmışdır

Removable storage cihazları üçün write access deaktiv edilmişdir

Audit policy subcategory override aktiv edilmişdir

Multicast name resolution deaktiv edilmişdir

Bu siyasətlər şəbəkə təhlükəsizliyini təmin etmək və sistem üzərində nəzarəti artırmaq məqsədilə tətbiq edilmişdir.

## 7.5 Digər departamentlər üçün standart GPO

HR, Finance və IT departamentlərindən fərqli olaraq digər departamentlər üçün standart təhlükəsizlik siyasəti tətbiq edilmişdir.

Bu siyasət aşağıdakı departamentlər üçün tətbiq edilmişdir:

Engineering

Marketing

Sales

Operations

Facilities

Legal

Customer Support

Bu departamentlər üçün tətbiq edilən standart GPO çərçivəsində aşağıdakı kompüter səviyyəli təhlükəsizlik parametrləri tətbiq edilmişdir:

Windows Defender Firewall aktiv edilmişdir

Multicast name resolution deaktiv edilmişdir

Removable storage cihazları üçün write access deaktiv edilmişdir

Bu siyasətlər sistem təhlükəsizliyini təmin etməklə yanaşı istifadəçilərin gündəlik iş fəaliyyətinə mane olmamaq məqsədilə tətbiq edilmişdir.

## 7.6 Default Domain Policy üzərində edilmiş dəyişikliklər

Domen səviyyəsində tətbiq olunan Default Domain Policy üzərində müəyyən təhlükəsizlik konfiqurasiyaları yoxlanılmış və bəzi parametrlər aktiv edilmişdir.

Bu siyasət çərçivəsində aşağıdakı təhlükəsizlik parametrləri tətbiq edilmişdir:

Microsoft Network Server – Digitally sign communications (always) aktiv edilmişdir

Domain member secure channel encryption aktiv edilmişdir

User Rights Assignment siyasətləri domen təhlükəsizlik modelinə uyğun şəkildə konfiqurasiya edilmişdir

Bu konfiqurasiyalar domen daxilində authentication və şəbəkə təhlükəsizliyinin təmin olunmasına xidmət edir.

## 7.7 Domain Wallpaper GPO

Domen mühitində istifadəçilər üçün vahid korporativ masaüstü görüntüsünü təmin etmək məqsədilə ayrıca GPO_Domain_Wallpaper siyasəti yaradılmışdır.

Bu siyasət vasitəsilə bütün istifadəçilərin masaüstünə aşağıdakı UNC path vasitəsilə paylaşılmış divar kağızı tətbiq edilmişdir.

\\ADDC\Wallpapers$\company-wallpaper.jpeg

Bu GPO-nun tətbiq edilməsinin məqsədi aşağıdakılardır:

korporativ mühitdə vahid vizual standartın təmin edilməsi

istifadəçilərin masaüstü görüntüsünün mərkəzləşdirilmiş şəkildə idarə olunması

şirkət brendinin bütün sistemlərdə tətbiq edilməsi

## 7.8 GPO strukturunun dizayn prinsipi

Layihə çərçivəsində Group Policy infrastrukturu hazırlanarkən sistem idarəetməsinin sadələşdirilməsi və təhlükəsizlik səviyyəsinin artırılması əsas məqsəd kimi götürülmüşdür. Bu səbəbdən GPO strukturu departamentlərin funksiyalarına uyğun şəkildə təşkil edilmişdir.

GPO-lar dizayn edilərkən aşağıdakı yanaşma tətbiq edilmişdir:

kritik departamentlər üçün ayrıca siyasətlərin yaradılması

digər departamentlər üçün standart siyasətin tətbiq edilməsi

domen səviyyəsində ümumi təhlükəsizlik siyasətlərinin saxlanılması

Bu yanaşma vasitəsilə həm təhlükəsizlik siyasətlərinin idarə edilməsi asanlaşdırılmış, həm də lazımsız GPO sayının artmasının qarşısı alınmışdır.

Kritik departamentlər (HR, Finance və IT) üçün ayrıca GPO-ların yaradılması həmin departamentlərin iş xüsusiyyətləri ilə əlaqədardır. Bu departamentlər sistem üzərində fərqli səlahiyyətlərə və təhlükəsizlik tələblərinə malikdirlər. Bu səbəbdən onların istifadəçi və sistem konfiqurasiyaları ayrıca siyasətlər vasitəsilə idarə olunur.

Digər departamentlər üçün isə ümumi təhlükəsizlik parametrlərini ehtiva edən standart GPO tətbiq edilmişdir. Bu yanaşma sistem idarəetməsini daha sadə və effektiv edir, eyni zamanda bütün istifadəçilər üçün vahid təhlükəsizlik standartını təmin edir.

Domen səviyyəsində isə bütün istifadəçilərə tətbiq olunan ümumi siyasətlər saxlanılmışdır. Bu siyasətlər domen mühitində təhlükəsizlik və konfiqurasiya sabitliyini təmin edir.

Bu struktur vasitəsilə Scarif Security domen mühitində Group Policy infrastrukturu həm təhlükəsizlik, həm də idarəetmə baxımından optimal şəkildə təşkil edilmişdir.

## 7.9 GPO siyasətlərinin client sistem üzərində test edilməsi

Yaradılmış Group Policy obyektlərinin client sistem üzərində düzgün tətbiq olunub-olunmadığını yoxlamaq məqsədilə domenə qoşulmuş Windows client sistemlər üzərində test aparılmışdır. Testlər HR və IT departamentlərinə aid istifadəçi hesabları ilə sistemə daxil olaraq həyata keçirilmişdir.

HR istifadəçisi ilə GPO testləri

HR departamentinə aid istifadəçi hesabı ilə sistemə daxil olduqdan sonra tətbiq olunan siyasətlərin işlədiyi yoxlanılmışdır.

Test zamanı aşağıdakı məhdudiyyətlərin tətbiq olunduğu müşahidə edilmişdir:

Command Prompt istifadəsi bloklanmışdır

PowerShell istifadəsi bloklanmışdır

Control Panel girişinə məhdudiyyət tətbiq edilmişdir

Bu nəticə HR departamenti üçün yaradılmış istifadəçi səviyyəli siyasətlərin client sistem üzərində uğurla tətbiq olunduğunu göstərir.

Domain Wallpaper siyasətinin yoxlanılması

Domain istifadəçisi ilə sistemə daxil olduqdan sonra masaüstü mühitinin avtomatik olaraq domen üzərindən paylaşılmış korporativ divar kağızı ilə dəyişdirildiyi müşahidə edilmişdir.

Wallpaper aşağıdakı UNC path vasitəsilə server üzərindən paylaşılmışdır.

\\ADDC\Wallpapers$\company-wallpaper.jpg

(Şəkil 7.9 – Domen istifadəçisi üçün tətbiq olunan masaüstü divar kağızı)

Bu nəticə göstərir ki GPO_Domain_Wallpaper siyasəti domen istifadəçilərinə uğurla tətbiq edilmişdir.

IT istifadəçisi ilə GPO testləri

IT departamentinə aid istifadəçi hesabı ilə sistemə daxil olduqdan sonra tətbiq olunan Group Policy obyektlərini yoxlamaq üçün aşağıdakı əmr istifadə edilmişdir.

### İcra olunan əmr

gpresult /r

### Əmr nəticəsində IT Organizational Unit üçün tətbiq olunan istifadəçi və kompüter səviyyəli Group Policy obyektləri siyahıya alınmışdır.

(Şəkil 7.X – IT client üzərində tətbiq olunan GPO-lar)

Test nəticəsində aşağıdakı vəziyyət müşahidə edilmişdir:

Command Prompt istifadəsi mümkündür

PowerShell istifadəsi mümkündür

sistem idarəetmə alətlərinə giriş açıqdır

Bu nəticə göstərir ki IT departamenti istifadəçiləri üçün digər departamentlərlə müqayisədə daha geniş sistem səlahiyyətləri verilmişdir.

# 8. IIS Server və Daxili Web Portalın Qurulması

## 8.1 IIS Web Server Rolunun Quraşdırılması

Scarif Security təşkilatının daxili web xidmətlərini təmin etmək məqsədilə Microsoft Internet Information Services (IIS) serveri qurulmuşdur. IIS server təşkilatın daxili portalının host edilməsi və əməkdaş məlumatlarının təqdim olunması üçün istifadə olunur.

Server üzərində IIS rolunun aktiv olduğunu yoxlamaq məqsədilə PowerShell vasitəsilə aşağıdakı əmr icra olunmuşdur:

Get-WindowsFeature -Name Web-Server

### Əmr nəticəsində sistem üzərində Web Server (IIS) rolunun quraşdırılmış olduğu müəyyən edilmişdir.

(Şəkil 8.1 – IIS server rolunun yoxlanılması)

## 8.2 IIS Saytlarının Konfiqurasiyası

IIS server üzərində mövcud web saytların siyahısını əldə etmək üçün aşağıdakı PowerShell əmri icra olunmuşdur:

Get-Website

### Əmr nəticəsində server üzərində iki web saytın mövcud olduğu müəyyən edilmişdir:

Təşkilatın daxili portalı ScarifInternalPortal adlı sayt vasitəsilə təqdim olunur.

(Şəkil 8.2 – IIS server üzərində mövcud saytların siyahısı)

## 8.3 Portalın Fiziki Fayl Strukturu

Portalın server üzərində yerləşdiyi qovluğu göstərmək üçün aşağıdakı PowerShell əmri icra olunmuşdur:

Get-ChildItem C:\WebApps\ScarifInternalPortal

### Əmr nəticəsində portalın aşağıdakı əsas komponentlərdən ibarət olduğu müəyyən edilmişdir:

Bu struktur portalın idarə olunmasını və gələcəkdə genişləndirilməsini asanlaşdırır.

(Şəkil 8.3 – Portal qovluq strukturu)

## 8.4 HTTPS Binding Konfiqurasiyası

Portalın təhlükəsizliyini təmin etmək məqsədilə IIS server üzərində HTTPS protokolu konfiqurasiya edilmişdir. HTTPS binding konfiqurasiyasını yoxlamaq üçün aşağıdakı PowerShell əmri icra olunmuşdur:

Get-WebBinding -Protocol https

### Əmr nəticəsində aşağıdakı binding konfiqurasiyası müəyyən edilmişdir:

Bu konfiqurasiya nəticəsində portal aşağıdakı ünvan vasitəsilə əlçatandır:

https://portal.scarif.local

(Şəkil 8.4 – IIS HTTPS binding konfiqurasiyası)

## 8.5 SSL Sertifikatının Tətbiqi

Portalın təhlükəsizliyini təmin etmək üçün IIS server üzərində SSL sertifikatı quraşdırılmışdır. Sertifikat Active Directory mühitində fəaliyyət göstərən daxili Certificate Authority tərəfindən yaradılmışdır.

Server üzərində mövcud sertifikatları yoxlamaq məqsədilə aşağıdakı PowerShell əmri icra olunmuşdur:

Get-ChildItem Cert:\LocalMachine\My

Nəticədə server üzərində aşağıdakı sertifikatın mövcud olduğu müəyyən edilmişdir:

Bu sertifikat IIS serverdə yerləşən portal üçün istifadə olunur və HTTPS bağlantısı vasitəsilə məlumatların şifrələnməsini təmin edir.

(Şəkil 8.5 – IIS server üzərində quraşdırılmış SSL sertifikatı)

## 8.6 Authentication Konfiqurasiyası

Portalın təhlükəsizliyini təmin etmək məqsədilə IIS server üzərində Windows Authentication mexanizmi aktiv edilmişdir. Bu konfiqurasiya nəticəsində yalnız Active Directory domen istifadəçiləri portala daxil ola bilir.

Windows Authentication konfiqurasiyasını yoxlamaq üçün aşağıdakı PowerShell əmri icra olunmuşdur:

Get-WebConfigurationProperty

-filter /system.webServer/security/authentication/windowsAuthentication

-name enabled

-PSPath IIS:\Sites\ScarifInternalPortal

### Əmr nəticəsində Windows Authentication parametrinin aktiv olduğu müəyyən edilmişdir.

(Şəkil 8.6 – IIS Windows Authentication konfiqurasiyası)

## 8.7 IIS Xidmətinin Statusu

IIS server üzərində web xidmətinin işlək vəziyyətdə olduğunu yoxlamaq məqsədilə aşağıdakı PowerShell əmri icra olunmuşdur:

Get-Service W3SVC

Yoxlama nəticəsində World Wide Web Publishing Service (W3SVC) xidmətinin aktiv və işlək vəziyyətdə olduğu müəyyən edilmişdir.

Bu xidmət IIS server üzərində web saytların işləməsini təmin edən əsas komponentdir.

(Şəkil 8.7 – IIS xidmətinin statusu)

## 8.8 Portalın Test Edilməsi və Təhlükəsizlik Analizi

IIS server üzərində qurulmuş daxili portalın düzgün işlədiyini və təhlükəsizlik mexanizmlərinin aktiv olduğunu yoxlamaq məqsədilə domenə qoşulmuş client kompüter üzərindən test aparılmışdır.

Portal istifadəçilər tərəfindən aşağıdakı daxili domen ünvanı vasitəsilə açılır:

https://portal.scarif.local

Portal Giriş Pəncərəsi

Portal açıldıqda istifadəçidən Active Directory domen hesabı ilə autentifikasiya tələb olunur. Bu autentifikasiya IIS server üzərində aktiv edilmiş Windows Authentication mexanizmi vasitəsilə həyata keçirilir.

İstifadəçi giriş pəncərəsində domen istifadəçi adı və parolu daxil edilir.

(Şəkil 8.12 – Portalın Windows Authentication giriş pəncərəsi)

Portalın Əsas Səhifəsi

Uğurlu autentifikasiyadan sonra istifadəçi portalın əsas səhifəsinə yönləndirilir. Bu səhifədə portalın dashboard hissəsi və təşkilatın daxili məlumatları göstərilir.

(Şəkil 8.13 – Scarif Internal Portal əsas səhifəsi)

Employee Directory Səhifəsi

Portal daxilində təşkilat əməkdaşlarının siyahısı Employee Directory bölməsində yerləşir. Bu bölmədə istifadəçilər əməkdaşların məlumatlarını görüntüləyə və axtarış edə bilirlər.

(Şəkil 8.14 – Employee Directory səhifəsi)

Employee Details Səhifəsi

Employee Directory bölməsində yerləşən View düyməsi vasitəsilə seçilmiş əməkdaş haqqında daha detallı məlumatları göstərən səhifəyə keçid edilir. Bu səhifədə əməkdaşın sistemdə saxlanılan əlavə məlumatları təqdim olunur.

Employee Details səhifəsi istifadəçilərə əməkdaşın identifikasiya məlumatlarını, aid olduğu departamenti və vəzifəsini daha ətraflı şəkildə görüntüləməyə imkan verir. Bu funksiya təşkilat daxilində əməkdaş məlumatlarının daha strukturlaşdırılmış şəkildə təqdim olunmasını təmin edir.

Bu mexanizm istifadəçilərə əməkdaşlar haqqında məlumatları sürətli və rahat şəkildə əldə etməyə imkan verir və daxili idarəetmə proseslərini sadələşdirir.

(Şəkil 8.15 – Employee Details səhifəsi (View funksiyası))

Təhlükəsizlik Analizi

Portalın təhlükəsizliyini təmin etmək məqsədilə aşağıdakı mexanizmlər tətbiq edilmişdir:

Windows Authentication

Portal anonim istifadəçilərə açıq deyil və yalnız Active Directory domen istifadəçiləri portala daxil ola bilir. Bu yanaşma istifadəçi identifikasiyasının mərkəzləşdirilmiş şəkildə idarə olunmasını təmin edir.

HTTPS Şifrələnməsi

Portal HTTPS protokolu üzərindən fəaliyyət göstərir və server üzərində quraşdırılmış SSL sertifikatı vasitəsilə istifadəçi ilə server arasında ötürülən məlumatlar şifrələnir. Bu mexanizm məlumatların üçüncü tərəflər tərəfindən ələ keçirilməsinin qarşısını alır.

Domen əsaslı giriş nəzarəti

Portal yalnız təşkilatın daxili şəbəkəsindən və domen istifadəçiləri tərəfindən əlçatandır. Bu isə sistemə kənar istifadəçilərin daxil olma riskini azaldır.

Beləliklə, aparılmış testlər göstərir ki IIS server üzərində qurulmuş Scarif daxili portalı düzgün işləyir və tətbiq edilmiş autentifikasiya və şifrələmə mexanizmləri sistemin təhlükəsizliyini təmin edir.

# 9. Nəticə

Bu layihə çərçivəsində Windows Server əsaslı korporativ şəbəkə infrastrukturu laboratoriya mühitində qurulmuş və onun əsas idarəetmə və təhlükəsizlik mexanizmləri praktik şəkildə tətbiq edilmişdir. Active Directory domen infrastrukturu yaradılmış, istifadəçilərin və sistem resurslarının idarə olunması üçün departament əsaslı Organizational Unit strukturu formalaşdırılmışdır.

İstifadəçi hesablarının yaradılması PowerShell skriptləri vasitəsilə avtomatlaşdırılmış, təhlükəsizlik idarəetməsi isə Security Group və RBAC modeli əsasında təşkil edilmişdir. File Server üzərində departament qovluqları yaradılmış və resurslara giriş hüquqları təhlükəsizlik qrupları vasitəsilə idarə olunmuşdur.

Group Policy mexanizmi vasitəsilə müxtəlif departamentlər üçün uyğun təhlükəsizlik siyasətləri tətbiq edilmiş və client sistemlər üzərində bu siyasətlərin düzgün işlədiyi test edilmişdir. Bundan əlavə, IIS server üzərində daxili korporativ portal qurulmuş və portal Active Directory autentifikasiyası və HTTPS şifrələnməsi ilə qorunmuşdur.

Aparılmış konfiqurasiyalar və testlər nəticəsində qurulan sistemin stabil və funksional şəkildə işlədiyi təsdiqlənmişdir. Layihə nəticəsində korporativ şəbəkə infrastrukturlarında istifadə olunan idarəetmə və təhlükəsizlik prinsipləri praktik olaraq tətbiq edilmiş və analiz olunmuşdur.
