<script>
import {Line} from "vue-chartjs";

export default {
    extends: Line,
    props: {
        label:{
            type: String
            },
            charData:{
                type: Array
            },
            options: {
                type: Object
            }
        },
        mounted(){
            const dates = this.charData.map(d => d.date).reverse()
            const totals = this.charData.map(d => d.total).reverse();

            this.renderChart(
                {
                    labels: dates,
                    datasets: [
                        {
                            label:this.label,
                            data:totals,
                        }
                    ]    
                },
                this.options
            );
    }
};
</script>