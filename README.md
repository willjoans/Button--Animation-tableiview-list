# Button--Animation-tableiview-list

@IBOutlet weak var btn3: UIButton!
@IBOutlet weak var btn2: UIButton!
@IBOutlet weak var btn1: UIButton!


func Action(Button1:UIButton,Button2:UIButton,Button3:UIButton){
        Button1.isSelected = true
        Button2.isSelected = false
        Button3.isSelected = false
    }
    @IBAction func TapToAction(_ sender: UIButton) {
        if sender == btn1{
            self.Str = "1"
            Action(Button1: btn1, Button2: btn2, Button3: btn3)
        }
        else if sender == btn2 {
            self.Str = "2"
            Action(Button1: btn2, Button2: btn1, Button3: btn3)
        }else{
            self.Str = "3"
            Action(Button1: btn3, Button2: btn2, Button3: btn1)
        }
        
    }
    //check-Uncheck Button
    
     @IBAction func TapToCheck(_ sender: UIButton) {
        if sender == self.btn5 {
            self.btn5.isSelected = !btn5.isSelected
            
            if btn5.isSelected{
                ArraySelected.append("5")
            }else{
               let str5 = ArraySelected.index(of: "5")
                ArraySelected.remove(at: str5!)
            }
        }
        
        
    //tableView RaDIO BUTTON method 
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return SelectedArry.count
    }
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell:StatiCRedioCell = tableView.dequeueReusableCell(withIdentifier: "Cell")as! StatiCRedioCell
        cell.lblName.text = SelectedArry[indexPath.row]
        cell.lblRadio.tag = indexPath.row
        cell.lblRadio.addTarget(self, action: #selector(TapToAction), for: .touchUpInside)
        let str = SelectedArry[indexPath.row]
        if str == Strcity{
            cell.lblRadio
                .setImage(UIImage(named: "selected_Card_btn"), for: UIControlState.normal)
            
        }else{
            cell.lblRadio
                .setImage(UIImage(named: "unselected_Card_btn"), for: UIControlState.normal)
        }
        return cell
    }
    func TapToAction(_ sender: UIButton){
      Strcity = SelectedArry[sender.tag]
      self.StaticRedioTableView.reloadData()
    }
    
    //////MULTIPLE CHECK
     func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return ArrayCheckBox.count
    }
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell:CheCkBoxCell = tableView.dequeueReusableCell(withIdentifier: "Cell")as! CheCkBoxCell
        
        let Bean = ArrayCheckBox[indexPath.row]
        cell.lblname.text = Bean.CateGoryName
        let CateImgUrl = URL(string:Bean.ImgUrl)
        cell.imgView.kf.setImage(with: CateImgUrl)
        cell.btnCheckBox.tag = indexPath.row
        
        let Str = Bean.CatId
        if SelectedArray.contains(Str){
            cell.btnCheckBox.setImage(UIImage(named: "instructor_checkbox_selected_05.png"), for: UIControlState.normal)
        }else{
            cell.btnCheckBox.setImage(UIImage(named: "instructur_checkbox.png"), for: UIControlState.normal)
        }
        return cell
    }
    //MARK:- Checkbox
    @IBAction func TapToCehckBox(_ sender: UIButton) {
        let Bean = ArrayCheckBox[sender.tag]
        let StrId = Bean.CatId
        
        if SelectedArray.contains(StrId){
            let ID = SelectedArray.index(of: StrId)
            SelectedArray.remove(at: ID!)
            
        }
        else{
            SelectedArray.append(StrId)
            //  print(SelectedArray)
        }
        self.CheckBoxTableView.reloadData()
        
    }
    
    
    /////Animation
    
     func StudentAnimation(){
        View_Table.transform = CGAffineTransform(scaleX: 0.2, y: 0.2)
        UIView.animate(withDuration: 0.3, delay: 0, options: [.transitionFlipFromTop, .allowUserInteraction, .curveLinear], animations: {() -> Void in
            
            self.View_Table.transform = .identity
            self.View_BG.superview?.bringSubview(toFront: self.View_Table)
            self.View_BG.isHidden = false
            self.View_Table.isHidden = false
            self.view.endEditing(true)
            
        }, completion: {(_ finished: Bool) -> Void in
            self.View_BG.backgroundColor = UIColor.clear.withAlphaComponent(0.7)
        })
    }
    
    
    ///Gusture
    
        let tap2 = UITapGestureRecognizer(target: self, action: #selector(handleTap))
        tap2.delegate = self as? UIGestureRecognizerDelegate
        View_BG.addGestureRecognizer(tap2)  
        
        
        @objc func handleTap(sender: UITapGestureRecognizer? = nil) {
        View_BG.isHidden = true
        
        View_Table.isHidden = true
    }
    
    
    
