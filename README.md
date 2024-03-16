Techno:
  -html tailwind.css(using web link so no need for manual install)
  -ajax method
  -php(preferable suing classes)
  -postgre
To do list:
  Page index(home)
    -front
      -aside navbar
        -home (home.html)
        -insert new role (insert.html)
        -delete role (delete.html)
      -tableau hierarchique
        -Button "modifier" (modify.html)
        -liste employe in the same niveau_hierarchique
    -database
      -table department(id,nom) 
      -table role(id,nom,niveau_hierarchique,id_department) NB: Assemblée générale niveau_hierarchique=1 & conseil niveau_hierarchique=2. one or the another but not below zero. AG & C department="High Management"
      -table v_role(id,nom,niveau_hierarchique,id_department,nom_department)
      -table employe(id,nom,id_role)
      -view v_employe(id,nom,id_role,nom_role,niveau_hierarchique,id_department,nom_department)
    -function
      -get_v_role
          return v_role from database
      -get_v_employe
          return v_employe from database
      -get_department
          retrun department from database
    -integration
        -fill tableau hierarchique w/ (get_role/get_employe)
        -if employe is null in tableau hierarchique. write "poste vacant"
        -if role is null in tableau hierarchique. don't show tableau

  Page modify
    -front
      -aside navbar
      -form
        -select employe value = employe id
        -button "promote"
        -select role value = role id
        -select department value = department id
        -button "fire"
        -button "confirm
     -database
      -table department
      -table role
      -table v_role
      -table employe        
      -vew v_employe
    -function
      -get_role
      -get_v_employe
      -get_department
    -integration
      -in select role, remove role employe is already in
      -in select department, remove department employe is already in
      -if employe niveau is equal to assemble general or conseil, department defaul value is assemble general or conseil
      -if button promote is clicked open select "role" & department
      -if button fire is clicked and select "role" is open, remove select "role" & "department"
      -if employe is fire, send info to treatment_employe.html w/ employe_id & role_id=null
      -if employe is promote, send info to treatment_employe.html w/ employe_id & role_id & department_id
        
  Page treatment_employe
    -front
    -database
      -table role
      -table department
      -table employe
      -view v_employe
    -function
      -delete_employe(id)
        delete row from employe where id(id)
      -update_employe
        update set role=
    -integration
      -if role_id=null, use delete_employe
      -if role_id!=null, user update_employe
      -head to result.html

  Page result
    -front
      "changement effectué"
      button "retourner à l'accueil"
    -database
    -function
    -integration

  Page insert
    -front
      -form
        text role
        number niveau
        select department
      -button "confirm"
    -database
      -table role
    -function
    -integration
      -if niveau >2 remove "select department" department=="High Management"
      -send info to treatment_insert w rolename,niveau & department

  Page treatment_insert
    -front
    -database
      table role
    -function
      -insert_role
    -integration
      -head to result.html
      
  Page delete
    -front
      -form
        select role
      -button "confirm"
    -database
      -table role
    -function
    -integration
      -send info to treatment_insert w (id_role,niveau & department)

  treatment_delete
    -front
    -database
      table role
    -function
      -delete_role(id_role,niveau, department)
      {
        lowest level = SELECT niveau_hierarchique from role ORDER BY niveau_hierarchique DESC LIMIT 1
        for(i;i<lowest level;i++){
          "DELETE row FROM employe WHERE niveau="+(niveau+i)
          "DELETE row FROM role WHERE niveau="+(niveau+i)
          if department!="high management"
            "DELETE row FROM role WHERE niveau="+niveau+i AND department=department"
        }
      }
    -integration
      -head to result.html
      
        
      
    
    
        
