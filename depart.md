ZxqDjAction action = (ZxqDjAction) myaction;
        
		//保存到T_SYS_DEPAR  和 T_DEPART_DETAIL 里面
		DepartDetail   operDepart = action.getOperDepart();
		TSysDepart  td = new TSysDepart();
		td.setDeparttype(operDepart.getDepartType());
		td.setLinkaddress(operDepart.getLinkAddress());
		td.setLinktel(operDepart.getLinkTel());
		td.setCity(operDepart.getCity());
		td.setUpdepartid(operDepart.getUpdepartId());
		td.setDescription(operDepart.getDescription());
		td.setState(operDepart.getState());
		
		if (StringUtils.isNotBlank(operDepart.getDepartName())) {
			td.setDepartnamePy(Char2spell.getPYString(operDepart.getDepartName()).toUpperCase());
			td.setDepartname(operDepart.getDepartName());
		}
		
		// 有上传图片，先保存上传的图片
		File photo = action.getLogoimage();
		if (photo != null) {
			// 有文件上传
			String str_maxphotosize = CommonQuery.getSysProperty(Constants.FILE_SIZE_PHOTO);// 系统参数管理里设置的图片最大大小
			long maxPhotoSize;
			if (StringUtils.isBlank(str_maxphotosize)) {
				maxPhotoSize = Constants.FILE_SIZE_1M;// 用系统默认，已经按字节计算
			} else {
				maxPhotoSize = Integer.parseInt(str_maxphotosize) * 1024;// kb转为字节
			}
			FileUtil.checkFileIsImage(action.getLogoimageContentType(), action.getLogoimageFileName());
			FileUtil.checkFileSize(photo.length(), maxPhotoSize);
			String relativeHttpPath = FileUtil.saveFile(photo, "cms", action.getLogoimageFileName());
			operDepart.setZxqct(relativeHttpPath);
		}
		
		if (StringUtils.isBlank(operDepart.getDepartId())) {
			long c = getBaseDao().count("select count(*) as c from TSysDepart a where a.departname = ? ",
					td.getDepartname());
			if (c > 0) {
				throw new Exception("此单位名称已经存在系统中！");
			}
			
			td.setDepartnamePy(DepartServiceImpl.getCheckedDepartnamePy(td.getDepartnamePy()));// 找到唯一的拼音
			
			if(StringUtils.isNotBlank(operDepart.getUpdepartId()))
			{
				td.setUpdepartid(operDepart.getUpdepartId());
			}
			//获取上级部门ID
			String deptid = getNewDepartid(td.getUpdepartid());
			td.setDepartid(deptid);
			//设置部门扩展信息的ID
			operDepart.setDepartId(deptid);
			td.setDepth(String.valueOf(deptid.length() / SysConstants.DEPART_CODE_STEP));
			getBaseDao().save(td);
			getBaseDao().save(operDepart);
			
			BusinessLogUtil.log(action.getUserloginid(), SysConstants.CZDX_T_SYS_DEPART, SysConstants.LOG_ACTION_SAVE,
					action.getRequest().getRemoteAddr());
		} 
		else 
		{
			long c = getBaseDao().count(
					"select count(*) as c from TSysDepart a where a.departname = ? and a.departid != ?",
					td.getDepartname(), operDepart.getDepartId());
			if (c > 0) {
				throw new Exception("此单位名称已经存在系统中！");
			}
			
			td.setDepartid(operDepart.getDepartId());
			
			//设置部门拼音，如果已经存在则在后面+1，递归检查，直到找个唯一的值
			td.setDepartnamePy(DepartServiceImpl.getCheckedDepartnamePy(td.getDepartnamePy()));// 找到唯一的拼音
			getBaseDao().updateNotNull(td);
			getBaseDao().updateNotNull(operDepart);
			BusinessLogUtil.log(action.getUserloginid(), SysConstants.CZDX_T_SYS_DEPART,
					SysConstants.LOG_ACTION_UPDATE, action.getRequest().getRemoteAddr());
		}
		
		