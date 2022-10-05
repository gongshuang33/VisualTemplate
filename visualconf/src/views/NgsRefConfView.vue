<template>
  <div class="ngs">
    <div>
		<div class="set-area">
			<div>[General]</div>
			<div>species = <input type="text" v-model="species"></div>
			<div>project_id = <input type="text" v-model="project_id"></div>
			<div>rootspace = <input type="text" v-model="rootspace"></div>
			<div>samplefile = <input type="text" v-model="samplefile"></div>
			<div>comparefile = <input type="text" v-model="comparefile"></div>
			<div>gtf = <input type="text" v-model="gtf"></div>
			<div>genome =  <input type="text" v-model="genome"></div>
			<div># DEG venn plot</div>
			<div >
				venn =  
				<input type="radio" name="radio-venn" value="no" v-model="venn" class="lab"  @change="display_input"><label>no</label>
				<input type="radio" name="radio-venn" value="yes" v-model="venn" class="lab"  @change="display_input"><label>yes</label> 
			</div>
			<div># leave it to 'no' if venn = no</div>
			<div>
				venn_info_txt = 
				<input type="radio" :class="{venn_info_display:isHidden,venn_info_hidden:isDisplay}" name="radio-venn-info" value="no" v-model="venn_info_txt" class="lab" disabled><label :class="{venn_info_display:isHidden,venn_info_hidden:isDisplay}">no</label>
				<input type="text" :class="{venn_info_display:isDisplay,venn_info_hidden:isHidden}" v-model="venn_info_txt_path" placeholder="Please input the path of venn_info.txt"> 
			</div>
			<div>[Annotation]</div>
			<div>annotseq = <input type="text" v-model="annotseq"></div>
			<div># cds or pep</div>
			<div>annotseq_type = 
				<input type="radio" name="radio-ann" value="cds" v-model="annotseq_type" class="lab" @change="annt"><label>cds</label>
				<input type="radio" name="radio-ann" value="pep" v-model="annotseq_type" class="lab" @change="annt"><label>pep</label> 
			</div>
			<div># 'f' for cds, 'p' for 'pep'</div>
			<div>annotseq_type_set = 
				<input type="radio" name="radio-s" value="f" v-model="annotseq_type_set" class="lab" @change="annt" disabled><label>f</label>
				<input type="radio" name="radio-s" value="p" v-model="annotseq_type_set" class="lab" @change="annt" disabled><label>p</label> 
			</div>
			<div>name2gene = <input type="text" v-model="name2gene"></div>
			<div># animal plant fungi</div>
			<div>species_type = 
				<input type="radio" name="radio-sp" value="animal" v-model="species_type" class="lab"><label>动物</label>
				<input type="radio" name="radio-sp" value="plant" v-model="species_type" class="lab"><label>植物</label> 
				<input type="radio" name="radio-sp" value="fungi" v-model="species_type" class="lab"><label>菌类</label> 
			</div>
		</div>
		<div class="view-area">

		</div>
		<div>
			<button class="copy" @click="GetConfTxt" v-clipboard:copy="copyText" v-clipboard:success="onCopy" v-clipboard:error="onError">COPY</button>
		</div>
	</div>
  </div>
</template>

<script>

export default {
	
	data() {
		return {
			species: '',
			project_id: '',
			rootspace: '',
			samplefile: '',
			comparefile: '',
			gtf: '',
			genome: '',
			venn: '',
			venn_info_txt: '',
			venn_info_txt_path: '',
			isDisplay: false,
			isHidden: true,
			annotseq: '',
			annotseq_type: '',
			annotseq_type_set: '',
			name2gene: '',
			species_type: '',
			copyText:''

		}
	},
	methods: { 
		display_input() {
			if(this.venn == 'yes') {
				this.isDisplay = true
				this.isHidden = false
				this.venn_info_txt = ''
			}
			if(this.venn == 'no') {
				this.isDisplay = false
				this.isHidden = true
				this.venn_info_txt = 'no'
			} 
			
		},
		annt() {
			if(this.annotseq_type == 'cds') {
				this.annotseq_type_set = 'f'
			}else if (this.annotseq_type == 'pep') {
				this.annotseq_type_set = 'p'
			}
		},
		onCopy(){
			alert("复制成功")
		},
		onError(){
			alert("复制失败")
		},
		GetConfTxt() {
			// this.copyText = 
		}
	}
	


}
</script>
<style>
	.set-area {
		border: 1px solid black;
		width: 90%;
	}
	.set-area > div {
		border: 1px dashed rgb(115, 228, 134);
		text-align: left;
		margin-left: 6px;
		height: 30px;
		line-height: 28px;
		border-left: none;
		border-right: none;
	}
	.set-area > div > input {
		width: 80%;
		border-right: none;
		border-left: none;
		border-top: none;
		border-bottom: 1px solid rgb(49, 155, 226);
		outline: none;
	}

	.set-area > div > .lab {
		width: auto;
		margin-left: 15px;
		border-right: none;
		border-left: none;
		border-top: none;
		border-bottom: 1px solid rgb(49, 155, 226);
		outline: none;
	}
	.venn_info_hidden {
		display:none;
	}
</style>
